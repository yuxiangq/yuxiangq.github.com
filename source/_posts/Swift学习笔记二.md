title: Swift学习笔记二
date: 2014-10-23 23:10:01
tags: [iOS,Swift]
---
Swift是一门类型安全的语言，Swift中包含的基础数据类型有以下7种

+ Int 整型，长度与当前平台的原生字长相同。在32位平台上，Int和Int32相同；在64位平台上和Int64相同。
+ Double 浮点型，表示64位浮点数。当你需要存储很大或者很高精度的浮点数时请使用此类型。
+ Float 浮点型，表示32位浮点数。精度要求不高的话可以使用此类型。
+ Bool 布尔型
+ String 字符串
+ Array 数组集合
+ Dictinary 词典集合

Swift中还包含Objective-C中不包含的高阶数据类型比如元组(Tuple)，用它可以很方便的通过一个函数返回多个值。

**声明常量和变量**
<pre><code>
//常量
let a=0
//变量
var b=1
</code></pre>

**类型标注**
<pre><code>
let num:Int = 1
let str:String = "test"
</code></pre>
*注意：*
*Swift支持类型推断，可以不用进行标注，Swift会根据你初始化该变量或常量使用的值，推断出类型。*

**Hello world**
<pre><code>
println(“hello world”)
</code></pre>
println是一个用来输出的全局函数，输出的内容会在最后换行。如果你用 Xcode，println将会输出内容到“console”面板上。(另一种函数叫print，唯一区别是在输出内容最后不会换行。)

与 Cocoa 里的NSLog函数类似的是，println函数可以输出更复杂的信息。这些信息可以包含当前常量和变量的值。

Swift 用字符串插值（string interpolation）的方式把常量名或者变量名当做占位符加入到长字符串中，Swift 会用当前常量或变量的值替换这些占位符。将常量或变量名放入圆括号中，并在开括号前使用反斜杠将其转义：
<pre><code>
let str="hello world"
println("this is \(str)") //this is hello world
</code></pre>

**类型安全和类型推断**

Swift 是一个类型安全（type safe）的语言。类型安全的语言可以让你清楚地知道代码要处理的值的类型。如果你的代码需要一个String，你绝对不可能不小心传进去一个Int。

当你定义变量或常量，如果你没有显式指定类型，Swift 会使用类型推断（type inference）来选择合适的类型。有了类型推断，编译器可以在编译代码的时候自动推断出表达式的类型。原理很简单，只要检查你赋的值即可。

**类型别名**

类型别名（type aliases）就是给现有类型定义另一个名字。你可以使用typealias关键字来定义类型别名。
<pre><code>
typealias MyInt=Int
var a:MyInt=0
</code></pre>

**元组**

元组（tuples）把多个值组合成一个复合值。元组内的值可以是任意类型，并不要求是相同类型。

下面这个例子中，(404, "Not Found")是一个描述 HTTP 状态码（HTTP status code）的元组。HTTP 状态码是当你请求网页的时候 web 服务器返回的一个特殊值。如果你请求的网页不存在就会返回一个404 Not Found状态码。
<pre><code>
let http404Error = (404, "Not Found")
// http404Error 的类型是 (Int, String)，值是 (404, "Not Found")
</code></pre>

并且可以很方便的将元组的内容分解
<pre><code>
let (statusCode, statusMessage) = http404Error
println("The status code is \(statusCode)")
// 输出 "The status code is 404"
println("The status message is \(statusMessage)")
// 输出 "The status message is Not Found"
</code></pre>
你可以在定义元组的时候给单个元素命名，给元组中的元素命名后，你可以通过名字来获取这些元素的值
<pre><code>
let http200Status = (statusCode: 200, description: "OK")
println("The status code is \(http200Status.statusCode)")
// 输出 "The status code is 200"
println("The status message is \(http200Status.description)")
// 输出 "The status message is OK"
</code></pre>
*注意：*
*元组在临时组织值的时候很有用，但是并不适合创建复杂的数据结构。如果你的数据结构并不是临时使用，请使用类或者结构体而不是元组。*

**可选类型(可空类型)**
使用可选类型（optionals）来处理值可能缺失的情况。可选类型表示：

+ 有值，等于 x

或者

+ 没有值

这个特性类似于C#中的可空类型，甚至表示方式都近似。
在我们与数据库交互的时候，可空值是非常重要的。因为数据库中的所有类型都是允许null的。

*注意：*
*C 和 Objective-C 中并没有可选类型这个概念。最接近的是 Objective-C 中的一个特性，一个方法要不返回一个对象要不返回nil，nil表示“缺少一个合法的对象”。然而，这只对对象起作用——对于结构体，基本的 C 类型或者枚举类型不起作用。对于这些类型，Objective-C 方法一般会返回一个特殊值（比如NSNotFound）来暗示值缺失。这种方法假设方法的调用者知道并记得对特殊值进行判断。然而，Swift 的可选类型可以让你暗示任意类型的值缺失，并不需要一个特殊值。*

来看一个例子。Swift 的String类型有一个叫做toInt的方法，作用是将一个String值转换成一个Int值。然而，并不是所有的字符串都可以转换成一个整数。字符串"123"可以被转换成数字123，但是字符串"hello, world"不行。

下面的例子使用toInt方法来尝试将一个String转换成Int
<pre><code>
let possibleNumber = "123"
let convertedNumber = possibleNumber.toInt()
// convertedNumber 被推测为类型 "Int?"， 或者类型 "optional Int"
</code></pre>
因为toInt方法可能会失败，所以它返回一个可选类型（optional）Int，而不是一个Int。一个可选的Int被写作Int?而不是Int。问号暗示包含的值是可选类型，也就是说可能包含Int值也可能不包含值。（不能包含其他任何值比如Bool值或者String值。只能是Int或者什么都没有。）

**if语句及强制解析**
可以使用if语句来判断一个可空值是否包含值。如果有值，则可通过在可空值变量后添加「感叹号」的方式获取该值，比如
<pre><code>
if convertedNumber != nil {
println("\(possibleNumber) has an integer value of \(convertedNumber!)")
} else {
println("\(possibleNumber) could not be converted to an integer")
}
</code></pre>
*注意：*
*使用!来获取一个不存在的可选值会导致运行时错误。使用!来强制解析值之前，一定要确定可选包含一个非nil的值。*

**可选绑定**
使用可选绑定重写上面的例子为
<pre><code>
if let actualNumber = possibleNumber.toInt() {
println("\(possibleNumber) has an integer value of \(actualNumber)")
} else {
println("\(possibleNumber) could not be converted to an integer")
}
// 输出 "123 has an integer value of 123"
</code></pre>
这段代码可以被理解为：

“如果possibleNumber.toInt返回的可选Int包含一个值，创建一个叫做actualNumber的新常量并将可选包含的值赋给它。”

如果转换成功，actualNumber常量可以在if语句的第一个分支中使用。它已经被可选类型包含的值初始化过，所以不需要再使用!后缀来获取它的值。在这个例子中，actualNumber只被用来输出转换结果。

你可以在可选绑定中使用常量和变量。如果你想在if语句的第一个分支中操作actualNumber的值，你可以改成if var actualNumber，这样可选类型包含的值就会被赋给一个变量而非常量。

*注意：*
*Swift 的nil和 Objective-C 中的nil并不一样。在 Objective-C 中，nil是一个指向不存在对象的指针。在 Swift 中，nil不是指针——它是一个确定的值，用来表示值缺失。任何类型的可选状态都可以被设置为nil，不只是对象类型。*