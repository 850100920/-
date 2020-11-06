## HTML与CSS学习

> 这篇文章主要讲了 CSS2D和3D转换 动画 和浏览器私有前缀
> 这是初学者看这个视频写下的笔记，如有错误，欢迎指正

## CSS 2D转换 (transform)

- CSS3新特性
- 实现元素位移，旋转，缩放
- 网页的坐标系和数学里面的不太一样 Y轴是向下的

### 移动 (translate)

- 和定位有点像
- 语法规范：

```css
div {
    transform: translate(x,y);
    transform: translateX(n);
    transform: translateY(n);
}
```

- 2d转换的优点： 不会影响其他元素的位置
- 实例：图片向上浮动的效果
- translate移动百分比是相对于自身元素的大小 (结合定位方法的垂直居中使用translate(-50%,-50%))
- 对行内标签没有效果

### 旋转 (rotate)

- 语法规范：

```css
div {
    tranform: rotate(10deg);
}
```

- 注意：rotate里面是度数 单位是deg
- 顺时针 正，逆时针 负
- 默认旋转中心是元素中心点

#### 修改旋转中心点 (transform-origin)

- 代码示例：

```css
div {
    transform-origin: x y;
}
```

- 注意：参数x和y用空格隔开
- 默认旋转中心为中心点 (50%,50%)
- 可以使用方位名词

#### 旋转练习

- 下拉三角的制作
- 代码样例:

> 感觉实际应用不会用这个，这个可以当作个练习

```html
<style>
    div {
        content: relative;
        width: 150px;
        height: 35px;
        border: 1px soild #fff;
    }
    div:after {
        content: absolute;
        width: 10px;
        height: 10px;
        border-right: 1px solid #000;
        border-bottom: 1px solid #000;
        transform: rotate(45deg);
    }
</style>
<body>
    <div></div>
</body>
```

- 旋转更换文字的背景颜色显示效果：

```html
<style>
    div {
        width: 200px;
        height: 200px;
        border: 1px solid #000;
        overflow: hidden;
    }
    div::before {
        content: '';
        /* 一定注意伪元素是行内块元素 */
        display: block;
        width: 100%;
        height: 100%;
        background-color: skyblue;
        transform-origin: left bottom;
        transform: rotate(180deg);
        transition: all .5s;
    }
    div:hover::before {
        transform: rotate(0deg);
    }
</style>
<head>
    <div></div>
</head>
```

### 缩放 (scale)

- 语法规范：

```css
div {
    transform: scale(x,y);
}
```

- 注意：其中的x和y用逗号分割
- x和y用数字，1代表一倍，2代表两倍
- x和y不加单位
- 如果只给一个参数，则宽度高度一起变
- scale的优势：
  - 正常修改宽高的话，高度会以顶边为基准
  - scale不会影响其他盒子，且可以设置缩放的中心点
- 修改缩放中心点和旋转的一样 (transform-origin)

#### 缩放实例

- 鼠标经过一个盒子，会出现图片被放大的情况
- 代码示例：

```html
<style>
    div {
        float: left;
        overflow: hidden;
    }
    div img {
        transition: all .4;
    }
    div img:hover {
        transform: scale(1.1);
    }
</style>
<body>
    <div>
        <img src="" alt="">
    </div>
</body>
```

- 分页按钮案例：每一个按钮鼠标经过时会放大
- 代码示例：

```html
<style>
    li {
        width: 30px;
        height: 30px;
        margin: 10px;
        border: 1px solid #999;
        text-align: center;
        line-height: 30px;
        list-style: none;
        border-radius: 50%;
        cursor: pointer;
        transition: all .2s;
    }
    li:hover {
        transform: scale(1.2);
    }
</style>
<body>
    <ul>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</body>
```

### 2D效果综合写法

- 代码示例：

```css
div {
    transform: translate() rotate() scale();
}
```

- 属性中间用空格隔开
- 顺序会影响转换的效果
- 同时有位移或着其他效果时，位移要放到前面
- 两个属性是同时进行的 (属性开始有先后顺序)

## CSS 动画 (animation)

- 制作动画流程：
  1. 先定义动画
  2. 在使用(调用)动画

### 利用keyframes定义动画

- 类似于定义类选择器
- 代码示例：

```css
@keyfreams 动画名称 {
    /* 开始状态 */
    0% {
        width: 100px;
    }
    /* 结束状态 */
    100% {
        width: 200px;
    }
}
```

- 动画序列:
  - 0%：动画开始 (from)
  - 100%：动画完成 (to)
- 0% 和 100% 之间可以分成很多个部分
- 百分比是时间的划分

### 元素使用动画

- 代码示例：

```css
div {
    /* 调用动画 */
    animation-name: 动画名称;
    /* 持续时间 */
    animation-duration: 持续时间;
}
```

- 注意：持续时间单位为秒

### 动画属性

| 参数                      | 说明                                                     |
| ------------------------- | -------------------------------------------------------- |
| animation-name            | 动画名称 **必须**                                        |
| animation-duration        | 完成一个周期花费的时间 **必须**                          |
| animation-timing-function | 动画速度曲线，默认为ease                                 |
| animation-delay           | 动画延迟开始，默认为0                                    |
| animation-iteration-count | 动画播放次数，无限循环infinite                           |
| animation-direction       | 动画在下一周期是否逆向播放，默认normal 逆向播放alternate |
| animation-play-state      | 动画暂停，默认running 暂停paused                         |
| animation-fill-mode       | 动画结束后的状态，保持forwards 回到起始backwards         |

#### 速度曲线细节

| 参数值      | 说明             |
| ----------- | ---------------- |
| linear      | 匀速             |
| ease        | 先快后慢         |
| ease-in     | 以低速开始       |
| ease-out    | 以低速结束       |
| ease-in-out | 以低速开始和结束 |
| steps()     | 步长 **重要！**  |

- 步长详解：
  - 动画从头走到尾需要多少步
  - 效果就变得一帧一帧的了 (可以制作打字机效果)

### 动画简写

- 代码示范：

```css
div {
    animation: 动画名称 持续时间 运动曲线 何时开始 播放次数 是否反向 是否返回起始点;
}
```

- 除了动画名称和持续时间剩下的都可以省略
- 注意：简写里面不包括animation-play-state (暂停属性)

### 动画案例

- 实现波纹的效果，可以用圆圈阴影从小变大实现
- 代码示例：

```html
<style>
    .point {
        position: absolute;
        top: 100px;
        right: 100px;
    }
    .dotted {
        width: 8px;
        height: 8px;
        background-color: #09f;
        border-radius: 50%;
    }
    .point div[class^="wave"] {
        position: absolute;
        /* 让阴影盒子和圆点在同一位置 */
        top: 50%;
        left: 50%;
        transform: translate(-50%);
        width: 8px;
        height: 8px;
        box-shadow: 0 0 12px #009dfd;
        border-radius: 50%;
        animation: pulse 1.2s linear infinite;
    }
    .point div.wave1 {
        animation-delay: 0;
    }
    .point div.wave2 {
        animation-delay: .4s;
    }
    .point div.wave3{
        animation-delay: .8s;
    }
    @keyframes pulse{
        0% {

        }
        70% {
            width: 40px;
            height: 40px;
            /* 透明度 */
            opacity: 1;
        }
        100% {
            width: 70px;
            height: 70px;
            opacity: 0;
        }
    }
</style>
<body>
    <div class="point">
        <div class="dotted"></div>
        <div class="wave1"></div>
        <div class="wave2"></div>
        <div class="wave3"></div>
    </div>
</body>
```

- 波纹没有使用scale缩放属性：缩放会连带着阴影大小一块缩放，很不美观
- 百度浏览器熊跑步的效果
- 百度的熊是一张长图片上有好几张运动状态的熊，用step来弄，每一帧放一个熊上去
- 注意，图片往左走的时候是负值
- 元素可以添加多个动画，用逗号隔开 (在第一个动画后面加逗号)

## CSS 3D转换 (transform)

- z轴往外为正，往里为负

### 3D位移 (translate3d)

- 可以沿着z轴方向移动
- 语法规范：

```css
div {
    /* 分别沿xyz轴移动 */
    transform: translateX(100px);
    transform: translateY(100px);
    transform: translateZ(100px);
    /* 混合写法 */
    transform: translate3d(x,y,z);
}
```

- 要是单个写的话注意后面的样式会覆盖前面的样式
- 但是可以这么写:

```css
div {
    transform: translateX(100px), translateY(100px);
    /* 推荐使用混合写法 */
}
```

- 混合写法时xyz不能省略，没有要写0
- 只移动z轴看不到效果，得结合透视一起才有效果

### 透视 (perspective)

- 想让网页中产生3D效果，需要透视
- 透视 == 视距，人眼到屏幕的距离 (近大远小)
- 透视要写在被观察元素的父盒子里
- 语法规范：

```css
/* 透视写在父盒子里 */
div {
    perspective: 500px;
}
```

### 3D旋转 (rotate3d)

- 除了坐标轴外，还可以沿着自定义轴旋转
- 语法规范：

```css
div {
    transform: rotateX(45deg);
    transform: rotateY(45deg);
    transform: rotateZ(45deg);
    /* 自定义轴 */
    transform: rotate3d(x,y,z,deg);
}
```

- rotate是沿着图片中心旋转的
- 旋转方向判断: 左手准则
  - 左手沿着坐标轴正方向, 四指弯曲的方向就是旋转正方向
- 使用的时候需要加透视才能看出3d效果
- 自定义轴: x,y,z可以取0到1, 表示是否希望沿这个轴旋转
  - 例如x=1, y=1 就是沿着对角线旋转

### 3D呈现 (transform-style)

- 控制子元素是否开启3D空间
- 代码示例:

```css
div {
    transform-style: flat | preserve-3d;
}
```

- flat: 默认值, 不开启3D空间
- preserve-3d: 子元素开启3D空间
- 代码写在父盒子里

#### 案例1: 两面反转的盒子

- 需求, 旋转之后颜色改变, 文字也改变
- 代码示例:

```html
<style>
    .box {
        width: 300px;
        height: 300px;
        margin: 0 auto;
        position: relative;
        transition: all .5s;
        transform-style: preserve-3d;
    }
    .front,
    .back {
        position: absolute;
        width: 100%;
        height: 100%;
        border-radius: 50%;
        font-size: 30px;
        text-align: center;
        color: #fff;
        line-height: 300px;
    }
    .front {
        background-color: pink;
        z-index: 1;
    }
    .back {
        background-color: purple;
        transform: rotateY(180deg);
    }
    .box:hover {
        transform: rotateY(180deg);
    }
</style>
<body>
    <div class="box">
        <div class="front">天王盖地虎</div>
        <div class="back">宝塔镇河妖</div>
    </div>
</body>
```

- 注意添加视距和3D呈现

#### 案例2: 3D导航栏

- 代码示例:

```html
<style>
    body {
        /* 旋转需要旋转box, 所以要给他的上一级写透视 */
        perspective: 500px;
    }
    .box {
        position: relative;
        width: 120px;
        height: 35px;
        transform-style: preserve-3d;
        transition: all .5s;
    }
    .front,
    .bottom {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
    }
    .front {
        background-color: pink;
        z-index: 1;
        /* 需要把这个盒子往前移,这样才能保证沿x轴旋转的时候不变型 */
        transform: translateZ(17.5px);
    }
    .bottom {
        background-color: purple;
        /* 这里注意: 旋转一定是负值 */
        transform: translateY(17.5px) rotateX(-90deg);
    }
    .box:hover {
        transform: rotateX(90deg);
    }
</style>
<body>
    <div class="box">
        <div class="front"></div>
        <div class="bottom"></div>
    </div>
</body>
```

- 旋转时一定要注意, 盒子是区分前后的, 所以一定注意正负

### 案例：照片旋转木马

- 展示实例(以后一定用到网页上)：

```html
<style>
    body {
        perspective: 1000px;
    }

    section {
        position: relative;
        width: 300px;
        height: 200px;
        margin: 100px auto;
        transform-style: preserve-3d;
        animation: rotate 10s linear infinite;
    }

    section div {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: url(image/background.jpg) no-repeat;
    }

    section div:nth-child(1) {
        transform: translateZ(300px);
    }

    section div:nth-child(2) {
        transform: rotateY(60deg) translateZ(300px);
    }

    section div:nth-child(3) {
        transform: rotateY(120deg) translateZ(300px);
    }

    section div:nth-child(4) {
        transform: rotateY(180deg) translateZ(300px);
    }

    section div:nth-child(5) {
        transform: rotateY(240deg) translateZ(300px);
    }

    section div:nth-child(6) {
        transform: rotateY(300deg) translateZ(300px);
    }

    @keyframes rotate {
        0% {
            transform: rotateY(0);
        }

        100% {
            transform: rotateY(360deg);
        }
    }

    section:hover {
        animation-play-state: paused;
    }
</style>
<body>
    <section>
        <div class=""></div>
        <div class=""></div>
        <div class=""></div>
        <div class=""></div>
        <div class=""></div>
        <div class=""></div>
    </section>
</body>
```

- 注意，这里要先旋转再移动，否则就会变成交叉再一块旋转

## 浏览器私有前缀

- 私有前缀为了兼容老版本的写法，新版无需添加
- 私有前缀：

| 参数值  | 说明                  |
| ------- | --------------------- |
| -moz-   | 火狐(firebox)         |
| -ms-    | IE                    |
| -webit- | safari 或 chrome 属性 |
| -o-     | Opera属性             |

- 圆角是有兼容问题
- 解决方法：

```css
div {
    -moz-border-raidus: 10px;
    -webkit-border-raidus: 10px;
    -o-border-raidus: 10px;
    border-radius: 10px;
}
```