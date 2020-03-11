---
title: mybatisExmple
tags:
  - mybatis
categories: 后端
date: 2019-07-24 13:26:13
---

# 简单查询
这个例子展示了如何用生成后的Example类去生成一个简单的where子句:
<!-- more -->
```  java
TestTableExample example = new TestTableExample();

example.createCriteria().andField1EqualTo(5); 
```
作为另一种选择, 下面的方式也是可以的:
``` java
TestTableExample example = new TestTableExample();

example.or().andField1EqualTo(5); 
```

在上面的例子中, 动态生成的where子句是:

``` sql
where field1 = 5
```

下面的例子展示了如何用生成后的Example类去生成一个复杂的where子句 (用到了 JSE 5.0 的泛型):

``` java
TestTableExample example = new TestTableExample();

example.or() 
.andField1EqualTo(5) 
.andField2IsNull();

example.or() 
.andField3NotEqualTo(9) 
.andField4IsNotNull();

List field5Values = new ArrayList(); 
field5Values.add(8); 
field5Values.add(11); 
field5Values.add(14); 
field5Values.add(22);

example.or() 
.andField5In(field5Values);

example.or() 
.andField6Between(3, 7);
```

在上面的例子中, 动态生成的where子句是:

``` sql
where (field1 = 5 and field2 is null) 
or (field3 <> 9 and field4 is not null) 
or (field5 in (8, 11, 14, 22)) 
or (field6 between 3 and 7) 
```

将会返回满足这些条件的记录结果.

# 去重复查询 
可以在所有的Example类中调用 setDistinct(true) 方法进行强制去重复查询.

## Criteria类 
Criteria 内部类的每个属性都包含 andXXX 方法，以及如下的标准的SQL查询方法:

IS NULL - 指相关的列必须为NULL 
IS NOT NULL - 指相关的列必须不为NULL 
= (equal) - 指相关的列必须等于方法参数中的值 
<> (not equal) - 指相关的列必须不等于方法参数中的值

> (greater than) - 指相关的列必须大于方法参数中的值 
= (greater than or equal) - 指相关的列必须大于等于方法参数中的值 
< (less than) - 指相关的列必须小于于方法参数中的值 
<= (less than or equal) - 指相关的列必须小于等于方法参数中的值 
LIKE - 指相关的列必须 “like” 方法参数中的值. 这个方法不用必须加入 ‘%’, 您必须设置方法参数中的值. 
NOT LIKE - 指相关的列必须 “not like” 方法参数中的值. 这个方法不用必须加入 ‘%’, 您必须设置方法参数中的值. 
BETWEEN - 指相关的列必须在 “between” 方法参数中的两个值之间. 
NOT BETWEEN - 指相关的列必须不在 “not between” 方法参数中的两个值之间. 
IN - 指相关的列必须在传入的方法参数的list中. 
NOT IN - 指相关的列必须不在传入的方法参数的list中.