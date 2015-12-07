title: UITableView实现下拉刷新
date: 2015-09-13 18:45:45
tags: [UITableView,iOS,下拉刷新]
---
**下拉刷新**实在是很了不起得创意。目前几乎所有APP只要涉及刷新的功能，都会采用这种方式，这已经是刷新交互的标配。

在Github上有大量的开源组件能实现**下拉刷新**和**上拉加载**，在这里我推荐**[MJRefresh](https://github.com/CoderMJLee/MJRefresh)**，它能帮我们很优雅的实现以上两种功能。

下拉刷新的原理，大家很容易理解，就是利用UITableView偏移到一定程度，然后调用刷新方法即可。但是有些童鞋可能发现了一个问题，就是UITableViewDelegate中并没有拖动相关的方法，这是怎么回事呢？其实那是因为UITableView本身继承自UIScrollView，所以我们只需要实现UIScrollViewDelegete中的- (void)scrollViewDidScroll:(UIScrollView * )scrollView方法即可。
<pre><code>
//只提供关键方法
-(void)p_InitUITableView
{
if(self.tableView==nil)
{
self.tableView=[UITableView alloc] init];
self.tableView.delegate=self;
self.tableView.datasource=self;
}
}
//拉动UITableView的时候会调用该方法
-(void)scrollViewDidScroll:(UIScrollView * )scrollView
{
//判断是否处于刷新状态
if(self.isLoading)
{
//获取实际内容的高度,及UITableViewCell集合的高度，包括超出屏幕部分。
float contentHeight=scrollView.contentSize.height;
//获取TableView的高度
float tableViewHeight=self.tableView.frame.size.height;
//获取展示内容的高度,如果内容高度大于UITableView高度，就以UITableView高度为准；
//如果内容高度小于UITableView高度，就以内容高度为准。
float displayHeight=contentHeight>tableViewHeight?tableViewHeight:contentHeight;
//接下来我们需要计算，我们拉动UITableView的时候，我们的展示内容displayHeight偏移了多少。
//假设相对于displayHeight往上或往下偏移20%的距离及算触发刷新。
if ((displayHeight - scrollView.contentSize.height + scrollView.contentOffset.y) / displayHeight > 0.2)
{
// 调用上拉加载方法，在这里可以处理一些刷新动画
}
//scrollView.contentOffset.y表示整个内容在y轴上的偏移量，下拉的时候内容是向y轴负方向移动
//所以计算的时候要取反
if (- scrollView.contentOffset.y / self.tableView.frame.size.height > 0.2)
{
// 调用下拉刷新方法，在这里可以处理一些刷新动画
}
}
</code></pre>
另外我们在添加下拉刷新的箭头的时候，Header不要添加在TableViewHeader上，要添加在UITableView的subView中。否则Header会一直在顶端，不会被覆盖。
