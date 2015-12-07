title: NumberTextField
date: 2015-01-12 20:46:26
tags: [iOS,自定义控件]
---
# [NumberTextField](https://github.com/yuxiangq/NumberTextField)
这是我做的一个只能输入数字的控件。
可以限制输入的数字长度及小数点位数。

## 使用方法
<script src="https://gist.github.com/yuxiangq/71a2ac1dabac7b4fa556.js"></script>
### 特性
* 去除数字前多余的0。例如，输入000123，当控件失去焦点，或者通过text获取值的时候，数字会被处理为123。
![image](https://raw.githubusercontent.com/yuxiangq/articlescreenshots/master/NumberTextField/before.png)
![image](https://raw.githubusercontent.com/yuxiangq/articlescreenshots/master/NumberTextField/after.png)

* 小数自动补0。例如，输入.123，当控件失去焦点，或者通过text获取值的时候，数字会处理为0.123。
![image](https://raw.githubusercontent.com/yuxiangq/articlescreenshots/master/NumberTextField/dotbefore.png)
![image](https://raw.githubusercontent.com/yuxiangq/articlescreenshots/master/NumberTextField/dotafter.png)

### 函数
<pre><code>
-(NSString*)trimText;
</code></pre>
调用该函数可以直接获取经过处理的数字。