# SW-Digital-backend

信永中和大数据技术部，后端初试（机试）题。

### ***题目讲解结束后，请自行创建腾讯会议，将会议号发送到拉钩，以便面试官随时查看。***

## 1、初试内容简介

### 时间：2小时15分钟

其中：

* 2小时机试（全程开启屏幕共享）
* 5分钟以内成果展示及(或)代码讲解
* 10分钟以内面试

> ***注意***
>
> ***在机试结束前，请务必将您的Code提交至fork的代码仓库中。***
>
> 面试过程有问题电话联系面试官。

## 2、题目

一道必做题，两道选做题

### 2.1 接口

1. 请为前端同学设计如下页面所需接口
2. 倒推数据库设计，创建数据库（数据库不限）
3. 实现接口（框架不限）

> 其中：
> 
> 日期选择为季度: Q1(1-3)，Q2(4-6)，Q3(7-9)，Q4(10-12)

![](https://sw-interview.oss-cn-beijing.aliyuncs.com/image/backend_api_interview.png)

### 2.2 算法

有一组长度为n的对象，每个对象里都有一个startTime和endTime，表示一个时间段。请面试者设计一个小算法，把这些对象中时间段存在重合关系的所有对象列出来。

### 2.3 SQL（选做）

Orders 表中存所有用户的订单信息。每个订单有唯一键 Id，Customer_Id 和 Business_Id 是 Users 表中 Users_Id 的外键。Status 是枚举类型，枚举成员为 (‘completed’, ‘cancelled_by_b’, ‘cancelled_by_c’)。

```
+----+-----------+-----------+---------+--------------------+----------+
| Id |Customer_Id|Business_Id| City_Id |        Status      |Request_at|
+----+-----------+-----------+---------+--------------------+----------+
| 1  |     1     |    10     |    1    |     completed      |2018-11-11|
| 2  |     2     |    11     |    1    |   cancelled_by_b   |2018-11-11|
| 3  |     3     |    12     |    6    |     completed      |2018-11-11|
| 4  |     4     |    13     |    6    |   cancelled_by_c   |2018-11-11|
| 5  |     1     |    10     |    1    |     completed      |2018-11-12|
| 6  |     2     |    11     |    6    |     completed      |2018-11-12|
| 7  |     3     |    12     |    6    |     completed      |2018-11-12|
| 8  |     2     |    12     |    12   |     completed      |2018-11-13|
| 9  |     3     |    10     |    12   |     completed      |2018-11-13| 
| 10 |     4     |    13     |    12   |   cancelled_by_b   |2018-11-13|
+----+-----------+-----------+---------+--------------------+----------+
```

Users 表存所有用户。每个用户有唯一键 Users_Id。Banned 表示这个用户是否被禁止，Role 则是一个表示（‘customer’, ‘business’, ‘partner’）的枚举类型。

```
+----------+--------+--------+
| Users_Id | Banned |  Role  |
+----------+--------+--------+
|    1     |   No   |business|
|    2     |   Yes  |customer|
|    3     |   No   |customer|
|    4     |   No   |customer|
|    10    |   No   |business|
|    11    |   No   |business|
|    12    |   No   |business|
|    13    |   No   |business|
+----------+--------+--------+
```

通过 SQL 查出 2018-11-11 至 2018-11-13 非Banned用户的取消率。

取消率 = （被取消的非Banned用户生成的订单数量) / (非Banned用户生成的订单总数)


```
+------------+-------------------+
|     Day    | Cancellation Rate |
+------------+-------------------+
| 2018-11-11 |       0.33        |
| 2018-11-12 |       0.00        |
| 2018-11-13 |       0.50        |
+------------+-------------------+
```

## 结果：
select o.Request_at Day,(round(count(if(status!="completed",status,null))/count(status),2) )  `Cancellation Rate` 
from  user u inner join orders o
on  u.User_ID = o.Customer_ID and  u.banned != 'Yes'
where  o.Request_at >= '2018-11-11' and  o.Request_at <= '2018-11-13'
group by  o.Request_at

祝您顺利
