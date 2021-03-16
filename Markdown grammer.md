# 标题:

我展示的是一级标题
=================

我展示的是二级标题
-----------------

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

# 段落

直接空行，或者两个空格  
像这样

# 字体
*斜体文本*
_斜体文本_
**粗体文本**
__粗体文本__
***粗斜体文本***
___粗斜体文本___

# 分割线

***

* * *

*****

- - -

----------

# 删除线
~~BAIDU.COM~~

# 下划线
<u>带下划线文本</u>

# 脚注

创建脚注格式类似这样 [^RUNOOB]。

[^RUNOOB]: 菜鸟教程 -- 学的不仅是技术，更是梦想！！！


# 列表
* 第一项
* 第二项
* 第三项

+ 第一项
+ 第二项
+ 第三项


- 第一项
- 第二项
- 第三项

1. 第一项
2. 第二项
3. 第三项

1. 第一项：
    - 第一项嵌套的第一个元素
    - 第一项嵌套的第二个元素
2. 第二项：
    - 第二项嵌套的第一个元素
    - 第二项嵌套的第二个元素

# 区块
> 最外层
> > 第一层嵌套
> > > 第二层嵌套

# 代码
`printf()` 函数

代码区块

    <'php
    echo 'RUNOOB';
    function test(){
        echo 'test';
    }
使用```包裹
```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```

# markdown链接

这是一个链接 [菜鸟教程](https://www.runoob.com)

<https://www.runoob.com>

这个链接用 1 作为网址变量 [Google][1]
这个链接用 runoob 作为网址变量 [Runoob][runoob]
然后在文档的结尾为变量赋值（网址）

  [1]: http://www.google.com/
  [runoob]: http://www.runoob.com/
  
# markdown图片

![alt 属性文本](图片地址)

![alt 属性文本](图片地址 "可选标题")

<img src="http://static.runoob.com/images/runoob-logo.png" width="50%">

# markdown表格

|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |

| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |

# 高级技巧
## 使用html元素
使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑

## 转义
**文本加粗** 
\*\* 正常显示星号 \*\*

## latex语法

$$E=mc^2$$
 导出为PDF、html带公式如下。enjoy！
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({ tex2jax: {inlineMath: [['$', '$']]}, messageStyle: "none" });
</script>