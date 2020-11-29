### HTML与CSS学习

> 这篇笔记主要记了CSS的基础语法，选择器，字体属性，文本属性，CSS三种引入方式
> 初学者写下的笔记，如有错误，欢迎大家前来指正。

### CSS基础

- CSS主要来美化网页
- CSS层叠样式表的简称(标记语言)

### CSS语法规范

- 选择器+{多条声明}
- 注释为`/* */`
- CSS要写在`<head>`里的`<style>`标签之中
- 代码示例(以p标签为例)：

```css
<style>
    p {
        color: red;
        font-size: 12px;
        /* 修改文字大小 */
    }
</style>
```

### CSS代码风格

- 样式格式
  - 紧凑格式:都写在一行上
  - 展开格式:展开书写(主流写法)
- 样式大小写: 默认小写
- 空格规范
  - 在冒号后面添加一个空格
  - 选择器和大括号之间保留一个空格

### CSS选择器

- 分类：
  - 基础选择器
    - 标签选择器
    - 类选择器
    - id选择器
    - 通配符选择器
  - 复合选择器(在demo5里)

#### 标签选择器

- 标签名作为选择器
- 优点:
  - 可以一次修改所有某一类的标签的样式
- 缺点:
  - 没法区分同名标签内的元素

#### 类选择器

- 单独选择一个或几个标签
- 语法样例：

```css
.类名 (class属性) {
    属性1: 属性值1;
}
```

- 标签中加class属性
- 无视标签，所有有相同class属性的都会改变样式
- 不能用标签名做class属性
- 有[前端命名规范](https://www.jianshu.com/p/6417143c4b18)
- css里的背景颜色`background-color`

##### 类选择器里的多类名

- 给一个标签指定多个类名(class)
- 代码示例

```html
<div class="red font35"></div>
```

- 多个类名中间用空格分开
- 能做到代码复用

#### id选择器

- 语法规范：

```css
#id名 {
    属性1: 属性值1;
}
```

- 和类选择器很像，只不过是把class改成id，.改成#
- 和类选择器的区别：
  - id只能调用一次，下面的在调用这个id就无法使用了

#### 通配符选择器

- 选取页面中所有的元素(标签)
- 代码示例:

```css
* {
    color: red;
    /* 把所有的标签都改为红色(包括html等标签) */
}
```

### CSS字体属性

#### 字体

```css
p {
    font-family: "微软雅黑";
}
h2 {
    font-family: "Microsoft YaHei",Arial;
}
```

- 可以选择多个字体，多个字体用逗号分割
- 一个字体有多个单词时尽量用引号
- 多个字体的目的，优先使用第一个字体，如果用户电脑上没有这个字体将使用下一个字体
- 如果这些字体都没有，使用浏览器自带字体
- chrome默认字体，微软雅黑

#### 字体大小

```css
p {
    font-size: 20px;
}
```

- 后面别忘了加px(像素)
- chrome浏览器文字默认大小16px
- 如果给body指明了文字大小，整个页面的文字的默认大小就改变了(标题大小不会改变，想要改变的话需要单独指明)

#### 字体粗细

```css
p {
    font-weight: normal | bold | bolder | lighter | number
}
```

- normal：正常字体，默认值
- blod：粗体
- bolder：特粗体
- lighter：细体
- number：数字 (后面不要加单位) **开发时常用**
  - 700加粗(bold)，400变细(nomal)
- 示例，标题在使用的时候经常去掉加粗

```css
h2 {
    font-weight: 400;
}
```

#### 文字样式

- 主要是斜体

```css
p {
    font-style: normal | italic;
}
```

- normal：普通样式，italic：斜体样式

#### 字体复合属性

- 示例：文字变倾斜，加粗，字号16，字体微软雅黑

```css
div {
    font: italic(font-style) 700(font-weight) 16px(font-size/line-hight) 'Microsoft yahei'(fonnt-family);
}
```

- 注意!顺序不能更换，里面各属性空格隔开
- 括号内是这个填写的属性
- 不需要的属性可以省略，但必须保留`font-size`和`font-family`属性，否则 font(整个css属性) 都不起作用

### CSS文本属性

- 文本外观，颜色，对齐，缩进，行间距

#### 文本颜色

```css
div {
    color: red;
}
```

- 预定义的值：各种英文单词
- 十六进制的值：#ff0000(red) **开发最常用**
- RGB写法：rgb(200,0,0)

#### 对齐文本

- 注：只能设置水平对齐格式

```css
div {
    text-align: center | left | right;
}
```

- left：左对齐 (默认值)
- right：右对齐
- center：居中对齐

#### 装饰文本

```css
p {
    text-decoration: none | underline | overline | line-through;
}
```

- none：默认值，没有装饰
- underline：下划线
- overline：上划线
- line-through：删除线

> 实例：去除链接的下划线

```css
a {
    text-decoration: none;
}
```

#### 文本缩进

- 文本首行缩进
- 可以取负值

```css
p {
    text-indent: 20px | 2em;
    /* 首行缩进20px */
    /* 2em是当前2个文字大小 */
}
```

- 单位em，em是一个相对单位，相当于当前一个元素的大小 **开发常用**

#### 行间距

- 控制行与行之间的距离

```css
p {
    line-height: 26px;
}
```

### CSS的引入方式

- css有三种样式表
  - 行内样式表(行内式)
  - 内部样式表(嵌入式)
  - 外部样式表(连接式)

#### 内部样式表

- CSS代码抽取出来，放到style标签中
- 理论上 style 可以放到任何地方，但默认放在 head 里

#### 行内样式表

- 直接在标签里面加上属性 style 就可以了
- 代码样例：

```html
<p style="color: pink; "></p>
```

- style是标签属性，只能控制当前标签

#### 外部样式表

- 使用较多的方法

- 在外部单独写一个css页面

- 操作步骤

  1. 新建一个.css文件
  2. 把之前在style标签里写的写在css文件里
  3. 在HTML页面中在 head 里写 `<link>` 标签来引入这个页面

  ```html
  <link rel="stylesheet" herf="css路径">
  ```

> 小知识：`<hr>`标签，水平线标签
> button标签，生成一个按钮
> 颜色#ff00ff，有两两相同的，可以省略为#f0f
> 不能直接给图片居中对齐，要对图片的父标签做居中对齐才有效

### chrome调试工具

- 左侧HTML，右侧CSS
- CSS里有黄色感叹号，有可能是属性写错了