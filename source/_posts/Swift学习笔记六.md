title: Swift学习笔记六
date: 2015-02-01 22:02:12
tags: [iOS,Swift]
---
Swift中的枚举拥有很棒的特性，至少以前我是没有接触过的。

####枚举语法####
使用**enum**关键字，并将其整个定义放在大括号内：
<pre><code>
enum demo{
//定义枚举相关类容
}
</code></pre>
假设我们定义指南针的四个方向：
<pre><code>
enum CompassPoint {
case North
case South
case East
case West
}
</code></pre>
一个枚举中被定义的值是枚举的**成员值**(或者**成员**)。
**case**关键字表明新的一样关键字被定义。

多个成员值也可以出现在同一行上，用逗号隔开：
<pre><code>
enum CompassPoint {
case North,South,East,West
}

//使用方法
var directionToHead = CompassPoint.West
directionToHead = .North
</code></pre>

> 注意：
不像 C 和 Objective-C 一样，Swift 的枚举成员在被创建时不会被赋予一个默认的整数值。在上面的CompassPoints例子中，North，South，East和West不是隐式的等于0，1，2和3。相反的，这些不同的枚举成员在CompassPoint的一种显示定义中拥有各自不同的值。

####相关值####
Swift的枚举可以存储任何类型的相关值，如果需要的话每个成员的数据类型是可以不同的。

比如我们可以定义两种商品条码的枚举：
<pre><code>
enum Barcode {
case UPCA(Int, Int, Int)
case QRCode(String)
}
</code></pre>
然后可以使用任何一种条码类型创建新的条码：
<pre><code>
var productBarcode = Barcode.UPCA(8, 85909_51226, 3)
productBarcode = .QRCode("ABCDEFGHIJKLMNOP")
//使用Switch-case
switch productBarcode {
case .UPCA(let numberSystem, let identifier, let check):
println("UPC-A with value of \(numberSystem), \(identifier), \(check).")
case .QRCode(let productCode):
println("QR code with value of \(productCode).")
}
</code></pre>
####原始值####
作为相关值的替代，枚举成员可以被默认值（称为原始值）预先填充，其中这些原始值具有相同的类型。

这是一个枚举成员存储原始ASCII的例子：
<pre><code>
enum ASCIIControlCharacter: Character {
case Tab = "\t"
case LineFeed = "\n"
case CarriageReturn = "\r"
}
</code></pre>
原始值可以是字符串，字符，或者任何整型值或浮点型值。每个原始值在它的枚举声明中必须是唯一的。当整型值被用于原始值，如果其他枚举成员没有值时，它们会自动递增。