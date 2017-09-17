title: MySqlParameter的坑
date: 2017-06-11 17:01:47
tags: [MySQL]
---

最近遇到一个MySQL相关的坑，这里简单记录一下。
在.Net中执行MySQL语句传参的时候我们一般使用MySqlParameter对象。于是在某个Dao层的方法中，我写了如下的语句：
```C#
var parms = new MySqlParameter[]
{
new MySqlParameter("?Type",(int)StatusType.Normal)
}
string sql = @"SELECT * FROM TABLE T WHERE T.Type = ?Type;";
```
结果是死活查不出数据，但是将SQL直接拿到服务器上运行，确能正常查出数据，实在是让人费解。随着不断调试，发现MySqlParameter的Value值不知为什么一直为null，后来试着改写了语句，用一个临时变量存储枚举值。
```C#
int type = (int)StatusType.Normal
var parms = new MySqlParameter[]
{
    new MySqlParameter("?Type",type)
}
string sql = @"SELECT * FROM TABLE T WHERE T.Type = ?Type;";
```
查询就正常了。

原来问题出在MySqlParameter的构造函数上，有两个关键的构造函数如下：
```C#
public MySqlParameter(string name, object value) { 
    // ...... 
} 
public MySqlParameter(string name, MySqlDbType type) { 
    // ...... 
    // MySqlDbType是个枚举类型 
}
```
我们第一次调用的时候，因为枚举为0，所以被当做第二个构造函数调用了。但是经测试当枚举不为0的时候，使用第一种调用方式，还是会使用第一种构造函数，确实令人看不懂。



