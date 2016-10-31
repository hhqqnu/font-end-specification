# 前端代码规范 及 最佳实践

编写本文档的主要驱动力是两方面： 
1. 代码一致性。 
2. 通过保持代码风格和传统的一致性，我们可以减少遗留系统维护的负担，并降低未来系统崩溃的风险。而通过遵照最佳实践，我们能确保优化的页面加载、性能以及可维护的代码。

## 工程文件

```
├── README.md //项目说明文件
├── dist //项目发布文件夹
├── package.json  //项目说明文档
└── src //项目源文件夹
    ├── css 
    ├── index.html
    ├── js
    │   ├── app
    │   │   ├── module1 //功能模块JS 1
    │   │   │   └── index.js
    │   │   ├── module2 //功能模块JS 2
    │   │   │   └── index.js
    │   │   └── module3 //功能模块JS 3
    │   │       └── index.js
    │   └── libs //第三方JS
    └── pages
        ├── module1 //功能模块页面 1
        │   └── index.html
        ├── module2 //功能模块页面 2
        │   └── index.html
        └── module3 //功能模块页面 3
            └── index.html
```
## HTML规范

### 整体结构
####HTML基础设施
- 文件应为标准的HTML5规范，首行以“<!DOCTYPE html>”
- 必须申请文档的编码charset，且与文件本身编码保持一致，使用UTF-8进行编码。
- 必须填写title标签，以表明本页面所实现的功能。
- 根据页面要求，设计页面所支持的viewport
- 页面中如使用HTML5新标签，需根据页面要求进行相应的兼容。

``` html
<!DOCTYPE html>
<html lang="zh-cn">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>html</title>
    <!--[if lt IE 9]>
      <script src="js/html5shiv.min.js"></script>
    <![endif]-->
  </head>
  <body></body>
  <script src="jquery.js"></script>
</html>
```
#### 结构顺序和视觉顺序基本保持一致
- 按照从上至下、从左到右的视觉顺序书写HTML结构。
- 用div代替table布局，可以使HTML更具灵活性，也方便利用CSS控制。
- table不建议用于布局，但表现具有明显表格形式的数据，table还是首选。

#### 结构、表现、行为三者分离，避免内联
- 使用link将css文件引入，并置于head中。
- 使用script将js文件引入，并置于body底部。

#### 保持良好的简洁的树形结构
- 每一个块级元素都另起一行，每一行都使用Tab缩进对齐（head和body的子元素不需要缩进）。删除冗余的行尾的空格。
- 建议使用4个空格代替1个Tab（大多数编辑器中可设置）。
- 也可以在大的模块之间用空行或注释隔开，使模块更清晰。


```
<body>
<!-- 侧栏内容区 -->
<div class="m-side">
    <div class="side">
        <div class="sidein">
            <!-- 热门标签 -->
            <div class="sideblk">
                <div class="m-hd3"><h3 class="tit">热门标签</h3> </div>
                ...
            </div>
            <!-- 最热TOP5 -->
            <div class="sideblk">
                <div class="m-hd3"><h3 class="tit">最热TOP5</h3> <a href="#" class="s-fc02 f-fr">更多»</a></div>
                ...
            </div>
        </div>
    </div>
</div>
<!-- /侧栏内容区 -->
</body>
```
#### 注，应该注意以下几点
- 结构上如果可以并列书写，就不要嵌套
`如果可以写成<div></div><div></div>那么就不要写成<div><div></div></div>`

- 如果结构已经可以满足视觉和语义的要求，那么就不要有额外的冗余的结构。
`比如<div><h2></h2></div>已经能满足要求，那么就不要再写成<div><div><h2></h2></div></div>`
- 一个标签上引用的className不要过多，越少越好。
`比如不要出现这种情况：<div class="class1 class2 class3 class4"></div>`
- 对于一个语义化的内部标签，应尽量避免使用className,可以使用"m-help li"。
`比如在这样一个列表中，li标签中的itm应去除：<ul class="m-help"><li class="itm"></li><li class="itm"></li></ul>
`

###代码格式
#### 注释方法
采用类似标签闭合的写法，与HTML统一格式；注释文案两头空格，与CSS注释统一格式。
- 开始注释：<!-- 注释文案 -->（文案两头空格）。
- 结束注释：<!-- /注释文案 -->（文案前加“/”符号，类似标签的闭合）。
- 允许只有开始注释！

```
<!-- 头部 -->
<div class="page-hd">
    <!-- LOGO -->
    <h1 class="page-logo"><a href="#">LOGO</a></h1>
    <!-- /LOGO -->
    <!-- 导航 -->
    <ul class="page-nav">
        <li><a href="#">NAV1</a></li>
        <li><a href="#">NAV2</a></li>
        <!-- 更多导航项 -->
    </ul>
    <!-- /导航 -->
</div>
<!-- /头部 -->
```
#### 代码本身的注释
单行代码的注释也保持同行，两端空格；多行代码的注释起始和结尾都另起一行并左缩进对齐。

```
<!-- <h1 class="page-logo"><a href="#">LOGO</a></h1> -->
<!--
<ul class="page-nav">
    <li><a href="#">NAV1</a></li>
    <li><a href="#">NAV2</a></li>
</ul>
-->
```
#### 严格的嵌套
- 尽可能以最严格的xhtml strict标准来嵌套，比如内联元素不能包含块级元素等等。
- 正确闭合标签且必须闭合。
#### 严格的属性
- 属性和值全部小写，每个属性都必须有一个值，每个值必须加双引号。
- 没有值的属性必须使用自己的名称做为值（checked、disabled、readonly、selected等等）。
- 可以省略style标签和script标签的type属性。

#####常用的标签
![](assets/标签.png)

###内容语义
#### 内容类型决定使用的语义标签
在网页中某种类型的内容必定需要某种特定的HTML标签来承载，也就是我们常常提到的根据你的内容语义化HTML结构。
#### 加强“资源型”内容的可访问性和可用性
在资源型的内容上加入描述文案，比如给img添加alt属性，在audio内加入文案和链接等等。
#### 加强“不可见”内容的可访问性
背景图上的文字应该同时写在html中，并使用css使其不可见或利用title属性，也可以在css失效的情况下看到内容。
#### 适当使用实体
以实体代替与HTML语法相同的字符，避免浏览解析错误。
常用HTML字符实体（建议使用实体）：

| 字符 | 名称 | 实体名 | 实体数 |
| --- | --- | --- | --- |
| " | 双引号 | &quot; | &#34; |
| & | &符 | &amp; | &#38; |
| < | 左尖括号（小于号） | &lt; | &#60; |
| > | 右尖括号（大于号） | &gt; | &#62; |
|  | 空格 | &nbsp; | &#160; |
|  | 中文全角空格 |  | &@12288; |

## CSS规范
## JS规范

