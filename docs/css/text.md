# 【Apple官网特效】iPhone 12 网页文字渐入效果

大家好，我是 Steven。

苹果网站向来是前端学习的好途径，最新发布的 iPhone 12 的产品介绍网页上就有一个**文字渐入效果**，这次我们会介绍这个效果是如何实现的。

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6f82cd91aff6409ebc697ca8bf93eba3~tplv-k3u1fbpfcp-watermark.image)

这个教学的视频版本在 [www.bilibili.com/video/BV1n5…](https://www.bilibili.com/video/BV1n54y1C7dt) ，欢迎一键三连并且关注！

## HTML 的部分

打开 CodePen 编辑器，先在 HTML 的部份加入一个标题。

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9c281e76b2c42f8a36c65a25a729771~tplv-k3u1fbpfcp-watermark.image)

## CSS 的部分

然后就可以专注在 CSS 的部份，加入 `body` 选择器，将背景颜色设定为黑色，`margin` 设定为 `0`，`display` 设定为 `flex`，`justify-content` 与 `align-items` 设定为 `center`，`min-height` 设定为 `100vh`，将内容于页面中上下左右置中。!



然后加入 `h1` 选择器，字体 `font-family` 设定为… 对，你猜对了，`Helvetica`。`margin` 和 `padding` 设定为 `0`，文字大小设定为 `48px`，颜色是白色。

再调整一下字于字之间的距离，`letter-spacing` 设定为 `0.3px`。

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c4ebc83dee15411d95cd5012fe9b98a2~tplv-k3u1fbpfcp-watermark.image)

然后关键就在这里，设定一个渐层颜色的背景，`background-image` 设定为 `linear-gradient()`，渐层的倾斜度是 `75deg`，颜色分为四段：

分别是两个白色，以及两个完全透明的白色，然后将 `background-size`，设定为水平方向是 `300%`，垂直方向是 `100%`。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9a5c4100ee1f4b5c8e6662db333068d4~tplv-k3u1fbpfcp-watermark.image)

这里的意思是，将背景的渐层颜色拉到三倍宽度，然后我们透过 `background-position-x` 调整它的位置。

`0%` 的话，就会看到整行文字都被白色覆盖，等于是渐层背景由 `0%` 至 `33.3%` 之间这一段的颜色： ![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f312686a4c6140088178d7b3cb1ab898~tplv-k3u1fbpfcp-watermark.image)

设定为 `50%` 的话，就是 `33.3%` 至 `66.67%` 之间这段颜色，所以是由白色渐变到透明色： ![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2f4a4c28301546eea52d1be4e03f5928~tplv-k3u1fbpfcp-watermark.image)

设定为 `100%`，就是 `66.67%` 到 `100%` 之间这段颜色。透明色至透明色，出来的结果也是透明色： ![img](data:image/svg+xml;utf8,<?xml version="1.0"?><svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="800" height="600"></svg>)

**所以我们只需要将这个 `background-position-x`，由 `100%` 动态改变为 `0%`，就可以做到文字渐入的效果。**

好了，明白了渐层颜色的原理后，就可以将渐层色套用到文字上。将 `background-clip` 设定为 `text`，然后将文字本身的颜色设定为透明 `transparent`。

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/728e8228e9a04f629f99bc63b5a3c637~tplv-k3u1fbpfcp-watermark.image)

然后加入 `h1:hover` 选择器，将 `background-position-x` 设定为 `0%`。最后，加入动画过渡的设定 `transition: 2s background-position-x ease-in-out`。

测试一下，现在已经可以做到这个文字渐入效果：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fd179b09310044ff9ed7242f1147bd2d~tplv-k3u1fbpfcp-watermark.image)

如果大家想这个渐入效果在页面卷动时才触发，我们可以进行一些改动。

## 在页面卷动的时候触发

首先在 HTML 里加入一个 `class` 名为 `sticky` 的 `<div>`，装着这个标题：

![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8a4fa9516bf14c34a71873ca3d610422~tplv-k3u1fbpfcp-watermark.image)

然后在 `body` 选择器内，移除 `flex` 的设定，将页面高度设定为例如 `3` 倍，`300vh`。

加入 `.sticky` 选择器，设定 `position` 是 `sticky`，`top` 是 `0`，即是当 `sticky` 这个 `<div>` 距离页顶 `0px` 时触发，贴着页面顶部。高度设定为 `100vh`，`display` 设定为 `flex`，`justify-content` 和 `align-items` 设定为 `center`：

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cbeb618d885f4d248d7469ad89a39ccf~tplv-k3u1fbpfcp-watermark.image)

在 JavaScript 的部份，加入 `document.addEventListener()` 监听页面卷动事件 `scroll`，然后建立一个变数，将 `document.documentElement.scrollTop` 除以 `scrollHeight` 减去 `clientHeight`，这样这个 `scrolled` 在页面卷动到底时是 `1`，卷动到顶时是 `0`：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1769278a2dff4d2fa5f3c63140dda314~tplv-k3u1fbpfcp-watermark.image)

然后要怎样在卷动的时候，更新 `background-position-x` 呢？加入 `const h1`，赋值为 `document.querySelector('h1')` 将 `h1` 获取回来。透过 `h1.style.setProperty()`，设定 `-percentage`，这个是我们自定义的 `CSS` 变数名，设定值是 `${scrolled * 100}%`：

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/358429b0465d4acfbe2cf0a14583b25f~tplv-k3u1fbpfcp-watermark.image)

在 CSS 的部份，加入 `:root` 选择器，初始化 `-percentage` 为 `0%`，然后 `background-position-x` 设定为 `calc(100% - var(--percentage))`，将 `transition` 和 `h1:hover` 的设定移除：

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/31a5fc6f88104477b9830e2edf42e5ab~tplv-k3u1fbpfcp-watermark.image)

![img](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3974bd907bfb416d8f6c2bed7f003aaa~tplv-k3u1fbpfcp-watermark.image)

## 我们来看看这个案例的完成效果

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0e74bfcee7e44cef9639efbcd9bd4e56~tplv-k3u1fbpfcp-watermark.image)

以上，就是今集要介绍的全部内容。


原文来源：https://juejin.cn/post/6908954433963425799

<iframe height="500px" style="width: 100%;" scrolling="no" title="vYyrebq" src="https://codepen.io/boyalexis/embed/vYyrebq?height=265&theme-id=dark&default-tab=result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/boyalexis/pen/vYyrebq'>vYyrebq</a> by Boyalexis
  (<a href='https://codepen.io/boyalexis'>@boyalexis</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>