---
title: "mysql比较日期"
categories: [MySQL]
tags: [corss join，datediff，timestampdiff]
---

## 0. 这篇解决什么
- 目标：解决mysql里面日期数据的比较
- 适用场景：当天数据与昨天比较
- 你可能踩的坑：datediff和timestampdiff的用法，结果是相反的

## 1. 核心概念
corss join：使用交叉联结会将两个表中所有的数据两两组合

datediff(日期1, 日期2)：得到的结果是日期1与日期2相差的天数。如果日期1比日期2大，结果为正；如果日期1比日期2小，结果为负。

timestampdiff(时间类型, 日期1, 日期2)：这个函数和上面diffdate的正、负号规则刚好相反。日期1大于日期2，结果为负，日期1小于日期2，结果为正。在“时间类型”的参数位置，通过添加“day”, “hour”, “second”等关键词，来规定计算天数差、小时数差、还是分钟数差。

## 2. 例子

```
Weather
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+

编写解决方案，找出与之前（昨天的）日期相比温度更高的所有日期的 id 。
返回结果 无顺序要求 。
结果格式如下例子所示

输入：
Weather 表：
+----+------------+-------------+
| id | recordDate | Temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+
输出：
+----+
| id |
+----+
| 2  |
| 4  |
+----+
解释：
2015-01-02 的温度比前一天高（10 -> 25）
2015-01-04 的温度比前一天高（20 -> 30）
```

```mysql
# Write your MySQL query statement below
select t.id id from Weather t
cross join Weather y
# datediff(日期1, 日期2)：得到的结果是日期1与日期2相差的天数。如果日期1比日期2大，结果为正；如果日期1比日期2小，结果为负。
#on datediff(t.recordDate ,y.recordDate )=1 
# timestampdiff(时间类型, 日期1, 日期2)：这个函数和上面diffdate的正、负号规则刚好相反。日期1大于日期2，结果为负，日期1小于日期2，结果为正。在“时间类型”的参数位置，通过添加“day”, “hour”, “second”等关键词，来规定计算天数差、小时数差、还是分钟数差。
on timestampdiff(day,y.recordDate,t.recordDate) = 1
where  t.temperature>y.temperature 
```




