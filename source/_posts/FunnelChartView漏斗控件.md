title: FunnelChartView漏斗控件
date: 2016-03-05 00:55:32
tags: [iOS,自定义控件]
---
FunnelChartView是我为满足产品需求编写的一个简单的漏斗图表控件，主要用来展示销售漏斗，使用CoreGraphics绘制而成。

一直在纠结，这个控件的数据应当采用什么结构传才好。于是做了两个初始化接口：

- 传一个FunnelChartModel列表。
- 传一个NSNumber列表，一个UIColor列表。

个人感觉还是似有不妥，另外控件的整体效果还不够精致，还需要更多的打磨。

具体效果如果：
![](https://raw.githubusercontent.com/yuxiangq/FunnelChartView/master/ScreenShots/Simulator%20Screen%20Shot%20Mar%203%2C%202016%2C%2022.50.16.png)

使用示例：
<script src="https://gist.github.com/yuxiangq/2ff50e3cfd49c0568844.js"></script>


