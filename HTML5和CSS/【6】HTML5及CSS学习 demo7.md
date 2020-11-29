## HTML与CSS学习

> 这篇文章主要讲了CSS的浮动部分，主要是有一个学成在线的案例学习到很多开发时的知识
> 案例请移步[学成在线案例](https://blog.csdn.net/weixin_46170034/article/details/104357836)
> 这篇笔记是初学者写下的笔记，如有错误，欢迎指正。

## 传统网页布局的三种方式

- 标准流(普通流/文档流)：按照默认的方式排列
- 浮动流
- 定位流

## CSS浮动

- 浮动可以改变元素标签的默认排列方式
- 网页布局第一准则：多个块级元素横向排列标准流，多个块级元素纵向排列浮动流

### 浮动详解

- float属性创建浮动框，使其移动到一边，直到左边缘或右边缘碰到另一个浮动框的边缘或父元素边缘

- 代码示例：

  ```css
  float: none | left | right;
  ```

| 值    | 描述               |
| ----- | ------------------ |
| none  | 元素不浮动(默认值) |
| left  | 元素向左浮动       |
| right | 元素向右浮动       |

### 浮动特性

1. 浮动的元素会脱离标准流

   - 脱离标准流的控制，移动到指定位置 (俗称脱标)
   - 浮动盒子不会保留原先的位置

   > 浮动是有浮动属性盒子会飘起来，后面没有浮动属性的盒子补上前面飘起来盒子位置

2. 浮动的元素会一行显示并且元素顶端对齐

   - 浮动元素会紧紧贴在一起 (不会有空隙)
   - 如果父元素宽度装不下这些盒子，多出的盒子会另起一行对齐

   > 可以这么理解：浮动的高度都是一样的，所以会并排显示

3. 浮动元素会具有行内块元素特性

   - 行内元素添加float属性可以设置宽高
   - 块元素添加float属性可以在一行显示
   - 添加浮动的行内元素和块元素，他的宽度根据内容宽度来确定

### 约束浮动元素策略

- 先用标准流父元素排列上下位置，之后内部子元素浮动来排列左右位置 (网页布局第一准则)
- 网页布局第二准则：先设置盒子大小，在设置盒子位置

### 浮动布局的注意点

- 和浏览器一样宽的盒子不需要指定宽度
- 元素浮动后只会影响后面的标准流，不影响之前的标准流
- 一个元素浮动了，其他的兄弟元素都应该浮动

### 清除浮动

#### 清除浮动的原因

- 有些父级盒子不方便给高度(如比较高的盒子，或者盒子高度要随时改变)，但是又不能不给高度(下面的标准流盒子又会占用父级盒子的位置)

#### 清除浮动的本质

- 清除浮动的本质是清除浮动元素对父级元素的影响
- 父盒子有高度，则不需要清除浮动
- 清除浮动以后，父级元素会自动检测盒子的高度，不会影响下面的标准流元素
- 语法规范：

```css
div {
    clear: left | right | both;
    /* 清除左浮动，清除右浮动，同时清除 */
}
```

- 在开发时几乎只用`clear: both;`

#### 清除浮动的方法

1. 额外标签法(隔墙法，但平时不常用) **W3C推荐**
2. 父级添加overflow属性
3. 父级添加after伪元素
4. 给父级添加双伪元素

##### 额外标签法

- 在父级盒子后面新建一个盒子(必须是块级元素)
- 在新建盒子里写上属性`clear: both;`
- 发现父元素能自动检测高度，不会影响后面的标准流元素
- 这种写法父盒子本身高度没有增加，而只是在浮动元素后增加一个盒子拦住下面标准流的元素

```html
<style>
    .nav {
        width: 100px;
        height: 100px;
        background-color: skyblue;
    }
    .clear {
        clear: both;
    }
</style>
<body>
    <div>
        <div class="nav"></div>
        <div class="nav"></div>
    </div>
    <div class="clear"></div>
</body>
```

- 优点：通俗易懂，书写方便
- 缺点：添加许多无意义的标签，结构性较差

##### 给父级添加overflow

- 给父元素添加overflow属性
- 这种方法父元素的高度会变得和子元素一样高，但是一旦有超出父元素边界的部分就会被隐藏
- 语法样例：

```html
<style>
    .box {
        overflow: hidden;
        /* 清除浮动 */
        width: 800px;
    }
    .nav {
        float: left;
        width: 400px;
    }
</style>
<body>
    <div class="box">
        <div class="nav"></div>
        <div class="nav"></div>
    </div>
</body>
```

- 优点：代码简洁
- 缺点：无法显示溢出的部分 (例如margin取负值)

##### after伪元素法

- 相当于额外标签法的升级版
- 语法规范：

```css
.clearfix:after {
    content: "";
    display: block;
    height: 0px;
    clear: both;
    visibility: hidden;
}
.clearfix {
    /* I6,I7专有 */
    *zoom: 1;
}
```

- 使用：在父元素上添加这个属性
- 例`<div class="nav clearfix">...</div>`

##### 双伪元素清除浮动 (最常使用)

- 语法规范：

```css
.clearfix:before,.clearfix:after {
    content:"";
    display:table;
    /* 如果写display:block的话两个块元素就会分行显示，影响父盒子大小 */
    /* table是表格，转化成块级元素并同行显示 */
}
.clearfix:after {
    clear:both;
}
.clearfix {
    *zoom:1;
}
```

- 使用方法和伪元素法一样，在父元素上加上这个属性

## PS切图模式

- jpg像素较高，常用于产品图片
- 图层切图：单击图层，选择快速导出为PNG
- 如果有多个元素想要导出为图片，合并两个图层(Ctrl+E)，然后导出
- 切片工具切图：
  1. 选中要切的部分
  2. 导出：文件->导出->储存为Web所用的格式，储存(储存时要选择选中的切片)
  3. 要导出背景透明的部分，关闭背景的眼睛，储存时选择png格式
- PS插件切图
  - 插件名：Cutterman
  - 导出选中的图层

## 学成在线案例

> 首页文件为index.html
> 外链样式表style.css

### CSS 属性书写顺序

- 建议顺序：
  1. 布局定位样式：display **默认第一个写，关系到元素样式** / position / float / clear / vidibilty
  2. 自身属性：width / height / margin / padding / border / background
  3. 文本属性：color / font / text-decoration / text-align / vertical-align / white-space / break-word
  4. 其他属性(CSS3)：content / cursor / border-radius / box-shadow / texte-shadow /…背景颜色rgba要放在这里(rgba为css3的属性)

### 页面布局思路

- 确定页面的可视区
- 分析页面的行模块，在数行模块里的列模块
- 每个行模块里面的列元素要用浮动布局，先确定大小再确定位置
- 制作HTML结构，遵循先有结构，后有样式的原则

#### 导航栏的实际操作方法

- 实际开发中不会直接用a标签，而是用li里面包含链接的方法
  - 原因：li语法更清晰
  - 如果直接使用a，搜索引擎会识别为有堆砌关键字的嫌疑，影响网站排名
- 代码示例：

```html
<style>
    .nav {
        float: left;
        margin-left: 60px;
    }

    .nav ul li {
        float: left;
    }

    .nav ul li a {
        display: block;
        padding: 0 10px;
        height: 42px;
        font-size: 18px;
        line-height: 42px;
    }
</style>
<body>
    <div class="nav">
        <ul>
            <li><a href="#">首页</a></li>
            <li><a href="#">课程</a></li>
            <li><a href="#">职业规划</a></li>
        </ul>
    </div>
</body>
```

- 注意事项，导航栏外面的盒子不要给宽度，里面内容是多宽外面的盒子就是多宽，方便以后添加文字
- 通常使用padding来指定每一个链接模块的宽度，看起来十分整洁
- button按钮默认有一个边框，需要手动去除
- 行内块元素中间默认有空隙
- 完整的代码案例在[demo7.html](https://blog.csdn.net/weixin_46170034/article/details/104357836)中