title: UICollectionViewController的用法
date: 2014-12-14 22:16:58
tags: [iOS,UICollectionViewController]
---
UICollectionView和UICollectionViewController是iOS6中新增加的控件，主要用于复杂的布局。你可以简单的把它理解为Grid。
在最近的版本中，我在做表单界面的时候，放弃了UITableViewController，改用UICollectionViewController来进行布局，个人感觉挺好用的，在这里我简单给大家分享一下UICollectionViewController的用法。

**首先请大家注意的是，记得为UICollectionView的collectionViewLayout属性设置UICollectionViewLayout的子类。否则是会报错的。**

UICollectionView的使用方式与UITableView相比没有什么区别，都是DataSource为View提供数据源，告诉View要显示什么东西以及如何显示他们，Delegate提供一些样式的小细节及用户交互的响应。

**初始化UICollectionView**
<script src="https://gist.github.com/yuxiangq/93fdc5d139747b410488.js"></script>
**UICollectionViewDataSource回调方法**
<script src="https://gist.github.com/yuxiangq/0c5aa8c4dd9ebc97047a.js"></script>
以上三个方法都是UICollectionViewDataSource的基本方法，这些方法在UITableViewDataSource中也是有的，所以使用起来难度不大。
另外我们需要注意的是控制Cell尺寸的方法并不在UIcollectionViewDelegate的回调中，而是在UICollectionViewDelegateFlowLayout中
<pre><code>
- (CGSize)collectionView:(UICollectionView * )collectionView layout:(UICollectionViewLayout* )collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath * )indexPath;
</code></pre>

关于UICollectionView中的Supplementary Views和Decoration Views我还没有用到。目前了解到的是Supplementary Views类似UITableView中的Header和Footer。Decoration Views用作背景展示。
因为UICollectionView比UITableView复杂得多，所以它的布局样式并不是通过Style来改变，而是通过UICollectionViewLayout，这也是UICollectionView的精髓所在。
