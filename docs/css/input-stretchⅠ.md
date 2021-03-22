# 纯CSSS3实现搜索框点击伸缩特效Ⅰ

话不多说，上效果图。

![](https://img-blog.csdn.net/20180418104935301)

核心代码就是 transition: cubic-bezier(0.68, -0.55, 0.27, 1.55) all 1s;\

![](https://img-blog.csdn.net/20180418110052772)

通过 transition 属性的 cubic-bezier（贝塞尔曲线） 在过渡效果上加了个缓冲效果。
html代码部分主要模块就是一个input 外加一个 父级 div  div宽度需要大于input宽度
不加 cubic-bezier 可以实现这个效果  transition: all 1s;

就是过渡效果少了个缓冲效果

我们这里使用到的运动曲线是

<img src="https://img-blog.csdn.net/20180418105619656" style="zoom:80%;" />

最后奉上完整代码
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <style type="text/css">
            .search-wrap{
                margin: 0 auto;
                width: 200px;
                height: 200px;
            }
            .search{
                width: 50px;
                height: 30px;
                margin: 20px 10px 0 0;
                border: 1px solid #4000FF !important;
                padding: 0 10px;
                float: right;
                border-radius: 5px;
                color: #fff;
                transition: all 1s;
                opacity: .5;
            }
            .search:focus{
                width: 100%;
                outline:none;
            }
        </style>
    </head>
    <body>
        <div class="search-wrap">
            <input type="text" name="" class="search">
        </div>
    </body>
</html>
```

