# 使用Jansson解析json格式

[toc]

## 介绍

Jansson是一个对json格式进行编码，解码，操作的c语言库，有以下特点

- 简单的api设计
- 文档详尽
- 无其他依赖库
- 完全支持UTF-8
- 大量的测试用例

Jansson是[MIT license](http://www.opensource.org/licenses/mit-license.php)源码发布方式

Jansson支持多个平台，包括Unix以及windows


## 编译安装

解压并编译

```shell
tar -xvf jansson-2.4.tar.gz
./configure --prifex=/newpan/cd/Install
make
make check
make install
```

windows平台可以支持vs2010及更新的版本。

## 简单使用

只需要包含一个头文件

```c
#include <jansson.h>
```
直接连接库方式编译

```shell
cc -o prog prog.c -ljansson
```

或者利用pkg-config

```shell
cc -o prog prog.c `pkg-config --cflags --libs jasson`
```

## 类型以及接口介绍

### 类型

Jasson主要使用的类型为

*json_t*

```c
enum json_type

JSON_OBJECT
JSON_ARRAY
JSON_STRING
JSON_INTEGER
JSON_REAL
JSON_TRUE
JSON_FALSE
JSON_NULL

int json_typeof(const json_t *json)


json_is_object(const json_t *json)
json_is_array(const json_t *json)
json_is_string(const json_t *json)
json_is_integer(const json_t *json)
json_is_real(const json_t *json)
json_is_true(const json_t *json)
json_is_false(const json_t *json)
json_is_null(const json_t *json)
```

### 引用计数

Jasson利用引用计数管理内存，下面两个接口进行引用计数的增加和减少

```c
json_t *json_incref(json_t *json)
void json_decref(json_t *json)
```

一般的操作是不会引起引用计数的变化的，需要人工进行增减，但是对于以`_new` 或者 `_new_`结束的可以自动对引用计数进行增减。


其他接口信息参见[API Reference](http://www.digip.org/jansson/doc/2.4/apiref.html#)

## 例子

根据[Tutorial](http://www.digip.org/jansson/doc/2.4/tutorial.html)摘抄如下

```
[
    {
        "sha": "<the commit ID>",
        "commit": {
            "message": "<the commit message>",
            <more fields, not important to this tutorial...>
        },
        <more fields...>
    },
    {
        "sha": "<the commit ID>",
        "commit": {
            "message": "<the commit message>",
            <more fields...>
        },
        <more fields...>
    },
    <more commits...>
]
```


```c

/*
 * Copyright (c) 2009-2012 Petri Lehtinen <petri@digip.org>
 *
 * Jansson is free software; you can redistribute it and/or modify
 * it under the terms of the MIT license. See LICENSE for details.
 */

#include <stdlib.h>
#include <string.h>

#include <jansson.h>
#include <curl/curl.h>

#define BUFFER_SIZE  (256 * 1024)  /* 256 KB */

#define URL_FORMAT   "https://api.github.com/repos/%s/%s/commits"
#define URL_SIZE     256

/* Return the offset of the first newline in text or the length of
   text if there's no newline */
static int newline_offset(const char *text)
{
    const char *newline = strchr(text, '\n');
    if(!newline)
        return strlen(text);
    else
        return (int)(newline - text);
}

struct write_result
{
    char *data;
    int pos;
};

static size_t write_response(void *ptr, size_t size, size_t nmemb, void *stream)
{
    struct write_result *result = (struct write_result *)stream;

    if(result->pos + size * nmemb >= BUFFER_SIZE - 1)
    {
        fprintf(stderr, "error: too small buffer\n");
        return 0;
    }

    memcpy(result->data + result->pos, ptr, size * nmemb);
    result->pos += size * nmemb;

    return size * nmemb;
}

static char *request(const char *url)
{
    CURL *curl;
    CURLcode status;
    char *data;
    long code;

    curl = curl_easy_init();
    data = malloc(BUFFER_SIZE);
    if(!curl || !data)
        return NULL;

    struct write_result write_result = {
        .data = data,
        .pos = 0
    };

    curl_easy_setopt(curl, CURLOPT_URL, url);
    curl_easy_setopt(curl, CURLOPT_WRITEFUNCTION, write_response);
    curl_easy_setopt(curl, CURLOPT_WRITEDATA, &write_result);

    status = curl_easy_perform(curl);
    if(status != 0)
    {
        fprintf(stderr, "error: unable to request data from %s:\n", url);
        fprintf(stderr, "%s\n", curl_easy_strerror(status));
        return NULL;
    }

    curl_easy_getinfo(curl, CURLINFO_RESPONSE_CODE, &code);
    if(code != 200)
    {
        fprintf(stderr, "error: server responded with code %ld\n", code);
        return NULL;
    }

    curl_easy_cleanup(curl);
    curl_global_cleanup();

    /* zero-terminate the result */
    data[write_result.pos] = '\0';

    return data;
}

int main(int argc, char *argv[])
{
    size_t i;
    char *text;
    char url[URL_SIZE];

    json_t *root;
    json_error_t error;

    if(argc != 3)
    {
        fprintf(stderr, "usage: %s USER REPOSITORY\n\n", argv[0]);
        fprintf(stderr, "List commits at USER's REPOSITORY.\n\n");
        return 2;
    }

    snprintf(url, URL_SIZE, URL_FORMAT, argv[1], argv[2]);

    text = request(url);
    if(!text)
        return 1;

    root = json_loads(text, 0, &error);
    free(text);

    if(!root)
    {
        fprintf(stderr, "error: on line %d: %s\n", error.line, error.text);
        return 1;
    }

    if(!json_is_array(root))
    {
        fprintf(stderr, "error: root is not an array\n");
        return 1;
    }

    for(i = 0; i < json_array_size(root); i++)
    {
        json_t *data, *sha, *commit, *message;
        const char *message_text;

        data = json_array_get(root, i);
        if(!json_is_object(data))
        {
            fprintf(stderr, "error: commit data %d is not an object\n", i + 1);
            return 1;
        }

        sha = json_object_get(data, "sha");
        if(!json_is_string(sha))
        {
            fprintf(stderr, "error: commit %d: sha is not a string\n", i + 1);
            return 1;
        }

        commit = json_object_get(data, "commit");
        if(!json_is_object(commit))
        {
            fprintf(stderr, "error: commit %d: commit is not an object\n", i + 1);
            return 1;
        }

        message = json_object_get(commit, "message");
        if(!json_is_string(message))
        {
            fprintf(stderr, "error: commit %d: message is not a string\n", i + 1);
            return 1;
        }

        message_text = json_string_value(message);
        printf("%.8s %.*s\n",
               json_string_value(sha),
               newline_offset(message_text),
               message_text);
    }

    json_decref(root);
    return 0;
}
```


## 参考

1. [Offical Doc](http://www.digip.org/jansson/doc/2.4/#)
2. [JSON Site](http://json.org/)
