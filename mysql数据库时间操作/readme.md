#### 获取当前时间

1. 获取当前时间+日期(date + time): now()

```sql
select now();
```

执行结果如下：

![](images/img-db1.png)

另外还有下面几个函数和now()函数的作用完全相同：
current_timestamp()、localtime()、localtime、


#### 附加项：为字段取别名

在查询数据时，为了使查询的结果显示的更加直观，我们可以为查询的字段取一个名字。

方式：

select 字段名 as 别名[,字段名 as 别名……] from 表名;

```
为字段指定别名，关键字as可以省略
```

```sql
select name as 部门名称 from department;
select name 部门名称 from department;
```

上面2条sql语句，分别为没有缺省as关键字方式为字段取别名和省略了关键字as的方式为字段取别名，执行结果相同：

![](images/img-db2.png)
