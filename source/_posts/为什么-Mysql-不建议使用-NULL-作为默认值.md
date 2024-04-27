---
title: 为什么 Mysql 不建议使用 NULL 作为默认值
date: 2024-04-27 16:46:05
tags: Mysql
---

#### NULL 和 '' 的区别
- `NULL` 代表一个不确定的值,就算是两个 `NULL`, 它俩也不一定相等。例如，`SELECT NULL=NULL` 的结果为 false，但是在我们使用 `DISTINCT,GROUP BY,ORDER BY` 时, `NULL` 又被认为是相等的
- '' 的长度是 0，是不占用空间的，而 `NULL` 是需要占用空间的
- `NULL` 会影响聚合函数的结果。例如，`SUM、AVG、MIN、MAX` 等聚合函数会忽略 NULL 值。 `COUNT` 的处理方式取决于参数的类型。如果参数是 `*(COUNT(*))`，则会统计所有的记录数，包括 `NULL` 值；如果参数是某个字段名 `(COUNT(列名))`，则会忽略 `NULL` 值，只统计非空值的个数
- 查询 `NULL` 值时，必须使用 `IS NULL 或 IS NOT NULLl` 来判断，而不能使用 `=、!=、 <、>` 之类的比较运算符。而 '' 是可以使用这些比较运算符的

所以在常用的开发中，Mysql 数据库中的字段默认值为 '' 比较好, 如果数据库中既有 NULL 也有 ''，则要小心避坑