# 泛型编程与stl笔记

## chapter 1

- stl的算法和容器是相互独立的
- 无须继承
- 效率高

## chapter 2

stl算法以iterator为基础

find使用iterator的原因

- 不必须为指针
- 区间内不必为数组元素

iterator必须有两个要求满足

- 有*操作可以获取值
- 有++操作可以向下遍历

concept表示一组类别的集合， 一组合法的程序

基本concept：赋值

- 构造函数
- 拷贝构造函数
- 比较：==, !=, >, <

同时满足这三个的为regular type

多数c++的类型都是regular type

iterator的5个concept：Input Iterator, Output Iterator, Forward Iterator, Bidirectional Iterator, Random Access Iterator

Input Iterator和Output Iterator均是一次遍历操作的迭代器

**24**