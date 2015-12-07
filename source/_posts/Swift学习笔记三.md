title: Swift学习笔记三
date: 2014-10-26 20:00:06
tags: [iOS,Swift]
---
这一部分主要了解运算符，因为大部分编程语言的运算符都相似，所以在这里我只记录有Swift特色的运算符。

###区间运算符###
Swift 提供了两个方便表达一个区间的值的运算符
####闭区间运算符####
闭区间运算符（a...b）定义一个包含从a到b(包括a和b)的所有值的区间，b必须大于a。 ‌ 闭区间运算符在迭代一个区间的所有值时是非常有用的，如在for-in循环中
<pre><code>
for index in 1...5  {
println("\(index) * 5 = \(index * 5)")
}
// 1 * 5 = 5
// 2 * 5 = 10
// 3 * 5 = 15
// 4 * 5 = 20
// 5 * 5 = 25
</code></pre>
####半开区间运算符####
半开区间（a..<b）定义一个从a到b但不包括b的区间。 之所以称为半开区间，是因为该区间包含第一个值而不包括最后的值。
<pre><code>
for index in 1...< 5  {
println("\(index) * 5 = \(index * 5)")
}
// 1 * 5 = 5
// 2 * 5 = 10
// 3 * 5 = 15
// 4 * 5 = 20
</code></pre>

###空合运算符###
空合运算符(a ?? b)将对可选类型a进行空判断，如果a包含一个值就进行解封，否则就返回一个默认值b.这个运算符有两个条件

+ 表达式a必须是Optional类型
+ 默认值b的类型必须要和a存储值的类型保持一致

<pre><code>
let defaultColorName = "red"
var userDefinedColorName:String?   //默认值为nil
var colorNameToUse = userDefinedColorName ?? defaultColorName
//userDefinedColorName的值为空 ，所以colorNameToUse的值为red
</code></pre>

实际上该运算符我在C#中早已接触过，确实是非常好用，配合可空类型，使代码相当优雅。



