title: 自定义UITableViewCell，使用VFL布局
date: 2015-04-12 20:57:39
tags: [iOS,UITableViewCell,VFL]
---

自定义UITableViewCell自动布局的文章网上又挺多的，但是大部分都是采用的xib进行布局，所以这一块其实水挺深的。经过自己的实践和不断的查找资料，终于实现了使用纯VFL布局，实现方式在这里和大家一起分享一下，[Demo比较简单](https://github.com/yuxiangq/UITableViewCell4VFL/commits?author=yuxiangq)

- 首先我们新建一个工程，命名为CustomCellWithVFLDemo，如下图所示：
![image](https://raw.githubusercontent.com/yuxiangq/articlescreenshots/master/CustomCellVFL/create_project_1.png)
![image](https://raw.githubusercontent.com/yuxiangq/articlescreenshots/master/CustomCellVFL/create_project_2.png)

- 让我们的ViewController继承UITableViewController。继承UITableViewController能帮我们省不少事情。
![image](https://raw.githubusercontent.com/yuxiangq/articlescreenshots/master/CustomCellVFL/viewcontroller_uitableviewcontroller.png)

- 新建CustomCell，我们在其中新建一个UILabel，叫contentLabel，用于展示文本数据并允许换行。
<script src="https://gist.github.com/yuxiangq/96c5ffeb2ab9d718a33e.js"></script>

- 为contentLabel设置约束，这里我们的约束可以看做Margin(5,5,5,5)。
<script src="https://gist.github.com/yuxiangq/dc9faab124f1eedf82a8.js"></script>

- 在ViewController中添加一个原型cell，动态计算高度的时候使用。
<script src="https://gist.github.com/yuxiangq/6c282d9899fe28fe59e4.js"></script>

<pre>
涉及换行的UILabel，请一定要注意**preferredMaxLayoutWidth**属性的设置，否则换行会出问题。
</pre>


