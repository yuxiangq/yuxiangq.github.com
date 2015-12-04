title: UITableViewCell的重用方法的区别
date: 2014-08-16 22:43:07
tags: iOS;UITableViewCell;UITableView
---
**UITableView**想必是iOS开发中最常用的控件。很多Apple自带的APP都使用了它，比如:*Phone*(该APP为典型得Tab结构,其中*Favorites*,*Recents*,*Contacts*都使用了**UITableView**)、*Messages*、*Mail*、*Settings*等等。

**UITableView**最基础的特性莫过于**UITableVIewCell**的重用。讲到这里不得不提我在实习的时候，负责的一个IM功能模块。当时在做聊天窗口的时候，用了ListView来显示聊天信息(这是基于.net平台的一个项目)，当收到聊天消息的时候我做的操作大致如下:
<pre><code>
public void ReceiveMeesage(string text)
{
TextBox txt=new TextBox();
txt.Text=text;
listBox.Items.Add(txt);
}
</code></pre>

或许大家已经看出问题了，随着消息越来越多Item中的控件会越来越多，内存消耗会越来越大，非常影响程序效率。
实际上我们并不需要那么多TextBox，假设聊天窗口一次能够展示10条消息，那么实际上我们只需要12个TextBox就能满足展示需要。没错，只需要复用TextBox就行了。在第一个TextBox移除我们视线之后，再将其从后载入，显示新的消息即可。

**UITableView**中实现Cell的重用是非常方便的，关键是DataSource中的两个方法，如下:
<pre><code>
-(id)dequeuReusableCellWithIdentifier:(NSString* )identifier; 
-(id)dequeueReusableCellWithIdentifier:(NSString* )identifier forIndexPath:(NSIndexPath* )indexPath NS_AVAILABLE_IOS(6_0);
</code></pre>
后者为**iOS6**加入的方法，两个方法的区别为:
**前者有可能从队列中返回nil，尤其是第一次执行的时候，Queue中没有任何Cell，需要我们手动创建，如下**:
<pre><code>
-(UITableViewCell * )tableView:(UITableView * )tableView cellForRowAtIndexPath:(NSIndexPath * )indexPath
{
static NSString * reuseIdentifier=@"cell";
UITableViewCell * cell=[tableView dequeueReusableCellWithIdentifier:reuseIdentifier];
if(!cell)
{
//在这里创建UITableViewCell
}
//设置你的Cell
return cell;
}
</code></pre>
**后者则不需要我们手动创建Cell，只需要提前注册一个原型Cell即可，假如Queue中没有Cell，程序会用原型Cell帮我们创建好，也就是不会出现返回nil的情况，代码如下:**
<pre><code>
-(void)viewDidLoad
{
//初始化UITableView的时候注册原型Cell
UITableView * tableView=[[UITableView alloc] init];
//调用[tableView registerNib:(UINib *) forCellReuseIdentifier:(NSString *)];
//或tableView registerClass:(__unsafe_unretained Class) forCellReuseIdentifier:(NSString *)
//注册原型Cell
self.view=tableView;
}

-(UITableViewCell * )tableView:(UITableView * )tableView cellForRowAtIndexPath:(NSIndexPath * )indexPath
{
UITableViewCell * cell=[tableView dequeueReusableCellWithIdentifier:reuseIdentifier forIndexPath:(NSIndexPath * )indexPath];
//设置你的Cell
return cell;
}
</code></pre>
在这里推荐用第二种方法，特别是当界面中有多种Cell的情况下，第二种方法在逻辑上更清晰。