title: Swift学习笔记五
date: 2015-01-01 17:29:59
tags: [iOS,Swfit]
---
# 函数的定义及调用
我们使用func关键字来定义函数:
<pre><code>

func test( / * 这里是函数参数，通常如此定义  parameter:String * / )->String{
return "test"
}

test() //调用函数
</code></pre>

# 默认参数值
给函数的参数定义默认值的方式和C#是一样的:
<pre><code>
func test(s:string= "defaultValue")->String {
return s;//如果s没有传值，则会返回defaultValue
}
</code></pre>

# 可变参数
用来输入不确定数量的参数，但是参数的类型必须一致:
<pre><code>
func test(numbers:Double...)->Double {
var total: Double = 0
for number in numbers {
total += number
}
return total
}
</code></pre>
**注意:一个函数至多能有一个可变参数，而且它必须是参数表中最后的一个。这样做是为了避免函数调用时出现歧义。**

# 常量参数和变量参数
这是要注意的是，函数中默认的参数为常量参数是不可以被重新赋值的。变量参数则需要显示定义。
<pre><code>
func test(s:String)->String{
s="test" //这里会报错，参数s为常量参数，不能被重新赋值
return s
}

func test(/ * 显示定位为变量 * /var s:String)->String{
s="test" //正常
return s
}
</code></pre>
**注意： 对变量参数所进行的修改在函数调用结束后便消失了，并且对于函数体外是不可见的。变量参数仅仅存在于函数调用的生命周期中。**

# 输入输出参数
这个和C#中的**ref,out**是类似的。如果你需要一个参数能在函数体内被修改，并且在函数调用结束后修改仍然存在，就需要使用**inout**关键字来定义参数。
<pre><code>
//交换两个变量的值
func swapTwoInts(inout a: Int, inout b: Int) {
let temporaryA = a
a = b
b = temporaryA
}
</code></pre>

# 函数类型
函数其实就是C#中的委托类型，也就是我们所说的函数指针。当然它相较于函数指针是类型安全的。
<pre><code>
func addTwoInts(a: Int, b: Int) -> Int {
return a + b
}

var mathFunction: (Int, Int) -> Int = addTwoInts //mathFunction就是指向addTowInts函数的变量
</code></pre>
如果我们要用一个变量来表示addTowInts这个函数，那么这个变量的类型就是**(Int, Int) -> Int**，可以读作“这个函数类型，它有两个 Int 型的参数并返回一个 Int 型的值。”。
函数类型也是可以作为函数参数或函数返回值的。

# 嵌套函数
默认情况下，嵌套函数是对外界不可见的，但是可以被他们封闭函数（enclosing function）来调用。一个封闭函数也可以返回它的某一个嵌套函数，使得这个函数可以在其他域中被使用。


