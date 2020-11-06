## HTML与CSS学习

> 这篇笔记主要讲了HTML5和CSS3的新特性
> HTML5新增了语义化标签，多媒体标签，input表单
> CSS3新增了属性选择器，结构伪类选择器(child类型，of-type选择器)，伪元素选择器，不受padding和margin影响的盒子模型，类似动画的过渡属性，模糊属性，和执行计算函数
> 这篇笔记是初学者写下的笔记，如有错误，欢迎前来指正

## HTML5新特性

- 有兼容性的问题，基本上在IE9以上才能使用

### HTML5新增语义化标签

- 终结了所有盒子都叫div
- 新增标签：

| 标签      | 描述             |
| --------- | ---------------- |
| <header>  | 头部标签         |
| <nav>     | 导航标签         |
| <article> | 内容标签         |
| <section> | 定义文档某个区域 |
| <aside>   | 侧边栏标签       |
| <footer>  | 尾部标签         |

- 在IE9使用需要转化成块级元素

### HTML5新增的多媒体标签

- 音频：<audio>
- 视频：<video>

#### 视频标签 (video)

- 只支持mp4(**支持的最多**)，webm，ogg
- 语法规范：

```html
<video src="文件地址" controls="controls"></video>
```

- 属性值：

| 标签     | 值                                  | 描述                                      |
| -------- | ----------------------------------- | ----------------------------------------- |
| autoplay | autoplay                            | 视频自动播放 (google浏览器禁用了这个属性) |
| controls | controls                            | 向用户展示播放控件                        |
| width    | px(像素)                            | 设置播放器宽度                            |
| height   | px(像素)                            | 设置播放器高度                            |
| loop     | loop                                | 播放完成后是否循环播放                    |
| preload  | auto(预加载视频) none(不预加载视频) | 是否预加载视频                            |
| src      | url地址                             | 视频url地址                               |
| poster   | image(图片)                         | 加载等待画面图片                          |
| muted    | muted                               | 静音播放                                  |

- 解决Google浏览器不能自动播放的问题，在autoplay的基础上添加muted属性 (muted=“muted”)
- controls一般用js解决

#### 音频标签 (audio)

- 支持音频格式：mp3(**支持的最多**) ，wav，ogg
- 语法规范：

```html
<audio src="文件地址" controls="controls"></audio>
```

| 标签     | 值       | 描述                                        |
| -------- | -------- | ------------------------------------------- |
| autoplay | autoplay | 音频自动播放 (google浏览器也禁用了这个属性) |
| controls | controls | 向用户展示播放控件                          |
| loop     | loop     | 循环播放                                    |
| src      | url      | 播放音频的位置                              |

- google禁用音频只能通过js来解决

### HTML5新增input表单

- input新增的type属性值：

| type属性值 | 描述            |
| ---------- | --------------- |
| email      | 输入为email类型 |
| url        | url类型         |
| date       | 日期            |
| time       | 时间            |
| month      | 月              |
| week       | 周              |
| number     | 数字            |
| tel        | 手机号码        |
| search     | 搜索框          |
| color      | 颜色选择表单    |

- 代码案例：

```html
<input type="email">
```

- 使用时如果内容错误，点击提交的时候会报错

#### HTML5新增表单属性

- 语法规范：

```html
<input required="required">
```

| 属性         | 值        | 描述                                                         |
| ------------ | --------- | ------------------------------------------------------------ |
| required     | required  | 表单拥有属性后不能为空，必填                                 |
| placeholder  | 提示文本  | 表单提示信息，存在默认值将不显示                             |
| autofocus    | autofocus | 自动聚焦属性，页面加载完成后自动聚焦到指定表单               |
| autocomplete | off / on  | 在当用户成功提交过，下次搜索就可以自动填充，默认为on，开发时改为off |
| multiple     | multiple  | 可以多选文件提交(经常和type="file"使用)                      |

- required同样在提交时报错
- 更改placeholder里文字的颜色：

```css
input::placeholder {
    color: skyblue;
}
```

## CSS3新特性

- 兼容性：IE9以上支持

### CSS3新增选择器

1. 属性选择器
2. 结构伪类选择器
3. 伪类选择器

#### 属性选择器 [ ]

- 选择元素有某个属性的标签
- 注意：属性选择器权重为10 (方括号内的才算属性选择器)
- 代码案例：

```html
<style>
    /* 选择input标签里有value属性的标签 */
    input[value] {
        color: skyblue;
    }
    /* 选择input标签value属性为select的标签 */
    input[value="select"] {
        color: red;
    }
</style>
<body>
    <input type="text" value="请输入用户名">
    <input type="text">
    <input type="text" value="select">
</body>
```

- 可以选择属性值开头的某些元素

```css
/* 选择那些div盒子里有class属性，且属性值以icon开头的元素 */
div[class^=icon] {
    color: blue;
}
```

- 选择某些属性值结尾的某些元素

```css
div[class$=icon] {
    color: grey;
}
```

- 选择值里面有这个文字的元素

```css
/* 只要是class属性里有icon值的都选出来 */
div[class*=icon] {
    color: green;
}
```

#### 结构伪类选择器

- 权重为10

##### child类型

- 代码示例：

```html
<style>
    ul li:first-child {
        /* 选择ul下面第一个叫li元素 */
        /* 相同的类型还有last-child，nth-child(n)；第n个元素，n可以是数字，关键字和公式 */
        background-color: skyblue;
    }
</style>
<body>
    <ul>
        <li><li>
        <li><li>
        <li><li>
        <li><li>
        <li><li>
    </ul>
</body>
```

- 实例：隔行变色
- 用到nth-child里的关键字 even-偶数 odd-奇数

```css
ul li:nth-child(odd) {
    background-color: grey;
}
```

- nth-child里面的公式 如果n是公式，则会从0开始计算，每次加一，但是第0个元素和超出的元素个数会被忽略

```css
ul li:nth-child(n) {
    background-color: grey;
}
```

- 注意：只能用n这个字母，但是可以使用加减乘除常数
- 例如 2n就选择偶数，n+5就是从第五个开始选择到最后

##### of-type类

- 语法规范

```css
ul li:first-of-type {}
ul li:last-of-type {}
ul li:nth-of-type(n) {}
```

- child类：
  - nth-child会把所有盒子排序
  - 然后先看nth-child(1)找到那个元素，然后再看前面它指定的标签，如果这两个不匹配，那么这个样式就不显现出来
- of-type类：
  - nth-of-type(1)会把指定元素排序
  - 然后再把第一个元素指定样式

#### 伪元素选择器

- CSS创建标签，不需要HTML标签
- 权重为 1

| 值       | 描述                       |
| -------- | -------------------------- |
| ::before | 在父元素内容的前面插入内容 |
| ::after  | 在元素内容的后面插入内容   |

- before和after创建一个行内元素
- 语法规范：

```css
div::before {
    color: skyblue;
    /* 必须书写的属性 */
    content: '';
}
```

- 注意：before和after必须有content属性 (类似于内容)
- before和after需要放到父元素的前面或后面
- 元素和::不能有空隙

##### 伪元素实例

- 搜索框后面的小箭头

```html
<style>
    .fake {
        width: 200px;
        height: 35px;
        border: 1px solid red;
        position: relative;
    }

    .fake::after {
        content: "^";
        /* 用定位来做，防止影响其他元素 */
        position: absolute;
        top: 10px;
        right: 0px;
    }
</style>
<body>
    <div class="fake"></div>
</body>
```

- 半遮罩层效果

```html
<style>
    .box::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0,0,0,.3);
    }
    /* 中间不能有空格 */
    .box:hover::before {
        display: block;
    }
</style>
<body>
    <div class="box"></div>
</body>
```

- 伪元素清除浮动 (在demo7里面)

### CSS3盒子模型 (box-sizing)

- 原来的盒子增加border，padding会撑大盒子
- CSS3解决了这个问题！
- 语法规范：

```css
div {
    box-sizing: content-box | border-box;
}
```

- content-box **默认值** 盒子大小为 width+padding+border
- border-box 盒子最终大小为width (padding和margin不要大于width宽度)
- 可以在CSS初始化时加上这个属性

### CSS3图片变模糊 (filter)

- CSS3新增的滤镜属性
- 语法规范：

```css
div {
    filter: 函数();
    /* 例：filter: blur(5px); blur模糊处理 ，数值越大越模糊 */
}
```

- 函数可以通过[MDN](https://developer.mozilla.org/zh-CN/)查询

### CSS3执行计算函数 (calc)

- 语法规范：

```css
div {
    width: calc(100%-80px);
}
```

- 使用场景，子盒子永远比父盒子小80px (用于经常改变宽度的父盒子)

### CSS3过渡属性 (transition)

- 经常和 :hover 一起使用
- 语法规范：

```css
div {
    transition: 要过渡的属性 花费时间 运动曲线 何时开始;
}
```

| 属性值       | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| 要过渡的属性 | 想要变化的CSS属性，高度宽度内外边距颜色都可以，所有属性都过渡写 all |
| 花费时间     | 单位秒(必须写单位)                                           |
| 运动曲线     | 默认ease (逐渐慢下来)                                        |
| 何时开始     | 单位秒，设置延迟触发时间(必须有单位) 默认0s                  |

- 注意：transition属性一定要写到开始变化的元素上
- 后面两个属性可以省略
- 同时修改两个属性(修改效果不同)时：

```css
div {
    transition: width .5s ease 1s, height .5s ease 1s;
}
```

- 修改效果相同时 选择属性写all

#### 过渡属性实例：进度条

- 代码示例：

```html
<style>
    .bar {
        width: 150px;
        height: 15px;
        border: 1px solid red;
        border-radius: 7px;
        padding: 1px 0;
    }

    .bar_in {
        width: 50%;
        height: 15px;
        background-color: red;
        border-radius: 7px;
        transition: all 1.5s;
    }

    .bar:hover .bar_in {
        width: 100%;
    }
</style>
<body>
    <div class="bar">
        <div class="bar_in"></div>
    </div>
</body>
```

#### 过渡属性实例 小米logo切换

- 代码案例：

```html
<style>
    .mi_box {
        width: 50px;
        height: 50px;
        background-color: #ff6700;
        margin: 100px auto;
        position: relative;
    }

    .mi_logo {
        position: absolute;
        top: 0;
        right: 0;
        transition: all .5s;
    }

    .mi_home {
        position: absolute;
        top: 0;
        right: -50px;
        transition: all .5s;
    }

    .mi_box:hover .mi_logo {
        right: 50px;
    }

    .mi_box:hover .mi_home {
        right: 0;
    }
</style>
<body>
    <div class="mi_box">
        <div class="mi_logo"><img src="image/mi-logo.png" alt="mi-logo"></div>
        <div class="mi_home"><img src="image/mi-home.png" alt="mi-home"></div>
    </div>
</body>
```