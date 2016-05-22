layout: eventkit
title: 如何创建Event
date: 2016-05-22 23:33:07
tags: [iOS,Eventkit]
---
因项目中有一个日程功能，个人认为和iOS中日历的事件(还有另一个东西叫提醒)挺相似的，于是决定将其数据和与系统日历事件同步，这样可以利用系统日历事件的提醒功能。
<pre>
**日历事件：**主要是时间为线索，将所有事件组织起来，事件或者说是行程安排是有时间先后顺序的。
**提醒事项：**功能和日历中的添加事件很相似，最大的不同在与条目的组织形式。提醒事项里的条目不再以时间顺序排列，而是可以对条目性质进行分类，如分成生活、工作、学习等等。或者也可以根据项目进行分类，且条目可以设置紧急程度。
**总结：**日历事件适合安排行程，提醒事项适用于项目的任务管理。</pre>

- 引入EventKit.framework。
- 创建EKEventStore
<pre>EKEventStore用于从用户的日历数据库中获取、创建、编辑和删除事件。</pre>
<script src="https://gist.github.com/yuxiangq/0741cd8a55832830e252cf12696699ad.js"></script>
- 创建CalendarEvent
<script src="https://gist.github.com/yuxiangq/f24490a827342d04f12138c9d8e5c22c.js"></script>
