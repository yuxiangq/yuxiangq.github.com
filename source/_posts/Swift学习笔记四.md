title: Swift学习笔记四
date: 2014-11-19 21:42:23
tags: [iOS,Swift]
---
Swift中的集合类型，数组和字典与Objective-C中相比，最大的不同就是**类型安全**。例如：如果我们创建了一个Int值类型的数组，我们就不能往其中插入任何不是Int类型的数据。

<pre><code>
//我们创建一个人员数组。
var employees : [String] = ["Jack","Mike"]
</code></pre>
实际上上面的数组我们利用Swift的推断特性，还可以写成这样
<pre><code>
var employees = ["Jack","Mike"]
</code></pre>
<pre><code>
//创建一个空数组
var array=Array<String>()
//或者
var array=[String]
</code></pre>

count属性用于后去数组的Item数量。
isEmpty属性可以快速的检测count是否为0。
append方法可以用于追加新的数据项。
for-in用于遍历数组。
我们可以使用+操作符来组合两个相同类型的数组。

字典在Swift中也是类型安全的，字典使用Dictionary<KeyType, ValueType>定义,其中KeyType是字典中键的数据类型，ValueType是字典中对应于这些键所存储值的数据类型。

KeyType的唯一限制就是可哈希的，这样可以保证它是独一无二的，所有的 Swift 基本类型（例如String，Int， Double和Bool）都是默认可哈希的，并且所有这些类型都可以在字典中当做键使用。

<pre><code>
//定义机场的缩写和全称
var airports: Dictionary<String, String> = ["TYO": "Tokyo", "DUB": "Dublin"]
//或者这样定义
var airports= ["TYO": "Tokyo", "DUB": "Dublin"]
</code></pre>

**如果集合遍历被定义为var，那么就是可变的。数组中的长度和其中的元素可以被修改，字典的长度和其中的元素也可以被修改。如果被定义为let，则不允许被修改。**


