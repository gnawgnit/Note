# CSS技巧

[TOC]

### css样式表引入

1. 行间引入：```<h1 style="color:red">hello world!</h1>```
2. head引入：```<head><style></style>style></head>>```
3. 外部引入：```<link rel="stylesheet" type="text/css" href="css.css">```

**ps:浏览器在检测到外部css文件后，开启另一线程。即异步的下载css html**

### 选择器

#### 派生选择器

```<li><strong>hello world!</strong></li>```

li strong{...}

#### id选择器(全文档只能使用一次，即只标记一个元素)

```<div id="identify"></div>```

#identify{...}

#### 类选择器

```<div class="class"></div>```

.class{...}

#### 元素选择器

span{...}

body{margin: 0; padding: 0;}

#### 属性选择器

[title]{...}

[title= #]{...}

[title~=#]{...}

[title|=#]{...}

#### 选择器分组

margin, h1, h2, h3, h4{......}

#### 后代选择器

**后代选择器（descendant selector）又称为包含选择器。**

**后代选择器可以选择作为某元素后代的元素。**

```<div class="header">this is a <em>paragraph</em></div>```

.class em{...}

#### 子元素选择器(缩小后代的范围，只选中该元素的子代)

**与后代选择器相比，子元素选择器（Child selectors）只能选择作为某元素子元素的元素。**

```<div class="header">This is a<em>example</em>,but the second<strong><em> "em"</em></strong> is not change</div>```

.header > em{...}

#### 相邻兄弟选择器

**如果需要选择紧接在另一个元素后的元素，而且二者有相同的父元素，可以使用相邻兄弟选择器**

h1 + p{...}

#### 伪类

**挺难记的**

下面是一个链接：[伪类](<https://www.w3school.com.cn/css/css_pseudo_classes.asp>)

#### 伪元素

[伪元素](<https://www.w3school.com.cn/css/css_pseudo_elements.asp>)





