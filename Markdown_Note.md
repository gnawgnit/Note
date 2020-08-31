# Markdown 语法

[toc]

## <span id="begin">1.标题</span>

```markdown
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题  同普通字体一样
```

## 2.字体属性

- 粗体

`**粗体**`：**粗体**

- 斜体

`*斜体*`：*斜体*

- 删除线

`~~删除线~~`：~~删除线~~

- 下划线

`<u>下划线</u>`：<u>下划线</u>

- 高亮

`=高亮=`：==高亮==

## 3.表格

```markdown
|name|sex|age|tele|
|--|--|--|---|
|汪婷|女|21|18388329876|
|wilbert|男|21|18326735467|
```

| name    | sex  | age  | tele |
| ---- | ---- | ---- | ------ |
| 汪婷    | 女   | 21   | 18388329876 |
| wilbert | 男   | 21   | 18326735467 |

## 4.列表

### 1.有序列表

```markdown
1. 段落1
2. 段落2
3. 段落3
```

1. 段落1
2. 段落2
3. 段落3

### 2.无序列表

`- `:color

- red
- green
- blue

## 5.代码块

### 1.行内代码块

C语言有一个函数叫`assert()`。

### 2.多行代码块

```markdown
​```c
	#include <stdio.h>
	int main(void){
		printf("hello world!");
		return 0;
	}
​```
```

```c
	#include <stdio.h>
	int main(void){
		printf("hello world!");
		return 0;
	}
```



## 6.分割线

`----`或`____`

----

______

## 7.超链接

语法格式：`[链接文字](链接地址 "链接标题")`

如：`[百度](www.baidu.com "baidu")`  效果：[百度](www.baidu.com "baidu")

再如：[点击此链接进入小黄网站](www.b43.cc "哈哈，可能要翻墙")

## 8.图片

语法格式：`![图片Alt](图片url "图片title")`。

图片Alt是指当图片无法正常显示时，就用定义好的图片Alt代替图片。

如：`![我的壁纸](D:/我的壁纸/1059834.png “鼠标在上面时显示的文字”)`

![我的壁纸](D:/我的壁纸/1059834.png "鼠标在上面时显示的文字")

## 9.引用

```markdown
> 一级引用
>
> > 二级引用
> >
> > > 三级引用
> > >
> > > > 四级引用
```

> 一级引用
>
> > 二级引用
> >
> > > 三级引用
> > >
> > > > 四级引用

## 10.空格

markdowm 不支持空格，需要用html标记`&nbsp;`。

`hello&nbsp;world`

hello&nbsp;world

## 11.字体、字号、颜色

markdown 不支持字体、字号、颜色，但是可以用html标记实现。

```markdown
<font face="黑体">这是黑体</font>
<font face="微软雅黑">这是微软雅黑</font>
<font face="宋体">这是宋体</font>

<font color="red">It's red</font>
<font color="blue">It's blue</font>
<font color="green">It's green</font>

<font size=23>23号字体</font>
<font size=8>8号字体</font>
<font size=3>浏览器默认字体大小</font>

<!--将字体属性font组合在一起-->
<font color="green" size=23 face="楷体">green 23 楷体</font>
```

<font face="黑体">这是黑体</font>
<font face="微软雅黑">这是微软雅黑</font>

<font face="宋体">这是宋体</font>

<font color="red">It's red</font>

<font color="blue">It's blue</font>
<font color="green">It's green</font>

<font size=23>23号字体</font>

<font size=8>8号字体</font>

<font size=3>浏览器默认字体大小 size=3</font>

<font color="green" size=23 face="楷体">green 23 楷体</font>

## 12.注脚和锚点

### 注脚

语法：`标注[^标注1]`标注[^标注1]

hello&nbsp;world![^2]

注脚放在文档最后。


### 锚点

当文章过于冗长，使用锚点可以在文章中快速定位

语法：`[说明文字](#jump)`建立跳转链接，`<span id="jump">跳转到的位置</span>`标记要跳转到的位置

[跳转到文章开始处](#begin)

[跳转到文章结尾处](#end)

## 13.目录结构

语法：`[toc]`按照标题级别显示目录

但是可能不支持跳转，要跳转的话，也可以使用锚点。如`[1.标题](#标题)<span id="标题">## 1.标题</span>`

但是很麻烦。

## 14.数学公式及符号

```markdown
$x^{y^z} = (1+e^x)^{-2xy^w}$
$log_{2}n$
$f(x,y)=100*\lbrace[(x+y)*3]-5\rbrace$
$\frac{1}{3}$
$\cfrac{1}{3}$
$\sqrt[3]{x}$
$\sqrt{5-x}$
```



$x^{y^z} = (1+e^x)^{-2xy^w}$

$log_{2}n$
$f(x, y) = 100 * \lbrace[(x + y)*3]-5\rbrace$

$\frac{1}{3}$
$\cfrac{1}{3}$
$\sqrt[3]{x}$
$\sqrt{5-x}$



------

**ps：其它符号大全**

![](D:/我的壁纸/符号大全1.jpg)

![](D:/我的壁纸/符号大全2.jpg)

![](D:/我的壁纸/符号大全3.jpg)

![](D:/我的壁纸/符号大全4.jpg)

<span id="end">**参考博客**[china_jeffery](https://blog.csdn.net/china_jeffery/article/details/78997984?utm_source=app)</span>

----

[^标注1]: 标注定义，标注解释
[^2]:你好世界！