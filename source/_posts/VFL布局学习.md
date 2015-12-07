title: VFL布局学习
date: 2014-12-04 23:17:14
tags: [iOS,VFL,自动布局]
---
随着iPhone6及iPhone6+的发布，适配大屏幕也提上了日程。有些童鞋习惯用xib配合iOS6时出现的autolayout进行界面的布局，但是我个人觉得xib实在是有点难用，特别是在macbook的小屏幕上，觉得xib要配一个大屏幕用起来才爽。还有就是用过Visual Studio的可视化编程后，始终觉得xib的易用性不够好。大屏幕又不得不适配，怎么办呢，如果像以前那样算坐标的话倒是也行，但毕竟比较繁琐，又不想用xib，那就只好用[Visual Format Language](https://developer.apple.com/library/ios/documentation/UserExperience/Conceptual/AutolayoutPG/VisualFormatLanguage/VisualFormatLanguage.html)。

初看VFL，肯定觉得莫名奇妙，给我的感觉就像第一次看到正则表达式的时候一样(个人以为VFL可比正则表达式简单多了)。不过VFL的符号比较少且简单，用2-3次估计就都记住了，大家可以看看上面官方文档的链接。我在这里简单介绍一下常用的符号表示的意思(我会用**方引号(「」)**将符号括起来)：

**「V:」**或**「H:」**分别表示垂直方向和水平方向。

**「|」**表示父视图。

**「[loginButton]」**表示一个名叫loginButton的视图

**「H:|-10-[loginButton]-10-|」** 表示 **loginButton在水平方向左边距离父视图10，右边距离父视图也是10**。

**「H:|-15-[buttonOne(80)]-5-[buttonTwo(90)]」** 表示**buttonOne在水平方向左边距离父视图是15，本身宽度是80，右边与buttonTwo的距离为5，buttonTwo的宽度为90**。

以上这些就是常用的符号，掌握着几种最基本的也足够我们进行大部分的界面布局了。
接下来我们简单写一个例子。我们假设大家都是有一定iOS编程基础的童鞋，所以怎么创建Single View Application这种事情就不罗嗦了，我们假设大家已经创建好了，接下来的我们将在View上添加一个Button，并用VFL来控制它的位置和大小。
<pre><code>
//我们在这里创建一个Buton
-(void)viewDidLoad
{
[super viewDidLoad];
UIButton* button=[[UIButton alloc] init];

//切记在这里一定要将该属性设置为NO，否则View
//会按照以往的autoresizingMask进行计算。
button.translatesAutoresizingMaskIntoConstraints=NO;

[button setTitle:@"测试" forState:UIControlStateNormal];
[self.view addSubview:button];
//当然，就这么执行程序是没有任何效果的，我们看不到Button出现在View上。

//用于存储约束
NSMutableArray *constraints = [NSMutableArray array];

//添加按钮的水平约束，意思是该按钮宽度90，距离父控件右边30。
[constraints
addObjectsFromArray:
[NSLayoutConstraint
constraintsWithVisualFormat:@"H:[button(90)]-30-|"
options:0
metrics:nil
views:NSDictionaryOfVariableBindings(
button)]];

//添加按钮的垂直约束，意思是该按钮高度40，距离父控件上边100。
[constraints
addObjectsFromArray:
[NSLayoutConstraint
constraintsWithVisualFormat:@"V:|-100-[button(40)]"
options:0
metrics:nil
views:NSDictionaryOfVariableBindings(
button)]];

//将约束添加到View中。
[self.view addConstraints:constraints];
}
</code></pre>
看完例子有木有觉得很简单，很有趣？