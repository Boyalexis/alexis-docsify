# 滚动视差

**视差滚动**（Parallax Scrolling）是指让多层背景以不同的速度移动，形成立体的运动效果，带来非常出色的视觉体验。 作为网页设计的热点趋势，越来越多的网站应用了这项技术。

![](https://user-gold-cdn.xitu.io/2018/8/10/16521e61a172b7d3?imageslim)

通常而言，滚动视差在前端需要辅助 Javascript 才能实现。当然，其实 CSS 在实现滚动视差效果方面，也有着不俗的能力。下面就让我们来见识一二：

## 认识 `background-attachment`

`background-attachment` 算是一个比较生僻的属性，基本上平时写业务样式都用不到这个属性。但是它本身很有意思。

`background-attachment`：如果指定了 `background-image` ，那么 `background-attachment` 决定背景是在视口中固定的还是随着包含它的区块滚动的。

单单从定义上有点难以理解，随下面几个 Demo 了解下 `background-attachment` 到底是什么意思：

### `background-attachment: scroll`

**scroll** 此关键字表示背景相对于元素本身固定， 而不是随着它的内容滚动。

### `background-attachment: local`

**local** 此关键字表示背景相对于元素的内容固定。如果一个元素拥有滚动机制，背景将会随着元素的内容滚动， 并且背景的绘制区域和定位区域是相对于可滚动的区域而不是包含他们的边框。

### `background-attachment: fixed`

**fixed** 此关键字表示背景相对于视口固定。即使一个元素拥有滚动机制，背景也不会随着元素的内容滚动。

> 注意一下 scroll 与 fixed，一个是相对元素本身固定，一个是相对视口固定，有点类似 `position` 定位的 `absolute` 和 `fixed`。

可以感受下 3 种不同取值的不同效果：

[CodePen Demo -- bg-attachment Demo](https://codepen.io/Chokcoco/pen/xJJorg)

## 使用 `background-attachment: fixed` 实现滚动视差

首先，我们使用 `background-attachment: fixed` 来实现滚动视差。**fixed** 此关键字表示背景相对于视口固定。即使一个元素拥有滚动机制，背景也不会随着元素的内容滚动。

这里的关键在于，即使一个元素拥有滚动机制，背景也不会随着元素的内容滚动。也就是说，背景图从一开始就已经被固定死在初始所在的位置。

我们使用，图文混合排布的方式，实现滚动视差，HTML 结构如下，`.g-word` 表示内容结构，`.g-img` 表示背景图片结构：

```html
<section class="g-word">Header</section>
<section class="g-img">IMG1</section>
<section class="g-word">Content1</section>
<section class="g-img">IMG2</section>
<section class="g-word">Content2</section>
<section class="g-img">IMG3</section>
<section class="g-word">Footer</section>
```

关键 CSS：

```css
section {
    height: 100vh;
}

.g-img {
    background-image: url(...);
    background-attachment: fixed;
    background-size: cover;
    background-position: center center;
}
```

效果如下：

![](https://user-gold-cdn.xitu.io/2018/8/10/16521e893d1a43ee?imageslim)

[CodePen Demo -- https://codepen.io/Chokcoco/pen/JBaQoY](https://codepen.io/Chokcoco/pen/JBaQoY)

嗯？有点神奇，为什么会是这样呢？可能很多人会和我一样，第一次接触这个属性对这样的效果感到懵逼。

我们把上面 `background-attachment: fixed` 注释掉，或者改为 `background-attachment: local`，再看看效果：

![](https://user-gold-cdn.xitu.io/2018/8/10/16521e3d6ef44adf?imageslim)

[CodePen Demo -- bg-attachment:local](https://codepen.io/Chokcoco/pen/ZjMdJz)

这次，图片正常跟随滚动条滚动了，按常理，这种效果才符合我们大脑的思维。

而滚动视差效果，正是不按常理出牌的一个效果，重点来了：

**当页面滚动到图片应该出现的位置，被设置了 `background-attachment: fixed` 的图片并不会继续跟随页面的滚动而跟随上下移动，而是相对于视口固定死了**。

好，我们再来试一下，如果把所有 `.g-word` 内容区块都去掉，只剩下全部设置了 `background-attachment: fixed` 的背景图区块，会是怎么样呢？

HTML 代码如下：

```html
<section class="g-img">IMG1</section>
<section class="g-img">IMG2</section>
<section class="g-img">IMG3</section>
```

``````css
section {
    height: 100vh;
}

.g-img {
    background-image: url(...);
    background-attachment: fixed;
    background-size: cover;
    background-position: center center;
}
``````

效果如下：

![](https://user-gold-cdn.xitu.io/2018/8/10/16521e6e9b9a54bc?imageslim)

[CodePen Demo](https://codepen.io/Chokcoco/pen/oMPrGZ)

结合这张 GIF，相信能对 `background-attachment: fixed` 有个更深刻的认识，移动的只有视口，而背景图是一直固定死的。

综上，就是 CSS 使用 `background-attachment: fixed` 实现滚动视差的一种方式，也是相对而言比较容易的一种。当然，`background-attachment: fixed` 本身的效果并不仅只是能有用来实现滚动视差效果，合理运用，还可以实现其他很多有趣的效果



原文来源：https://juejin.cn/post/6844903654458146823#heading-5