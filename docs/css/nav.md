# 学校网站通用nav导航栏

?> 背景知识：[animation]()，[keyframes]()

效果：

源码：

```html
<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset='UTF-8'>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        .nav {
            height: 55px;
            width: 100%;
            background-color: #0b6cb8;
        }
        ul {
            width: 80%;
            margin: 0 auto;
            list-style: none;
            display: flex;
        }
        li {
            height: 55px;
            width: 150px;
            text-align: center;
            flex: 1;
            flex-shrink: 0;
            line-height: 52px;
        }
        a {
            text-decoration: none;
            color: #fff;
            font-size: 15px;
            display: block;
        }
        li:hover {
            background-color: #0a5894;
        }
        li>dl {
            display: none;
            background-color: #0a5894;
            /* animation: cool 0.3s linear 0s forwards; */

        }
        dd:hover {
            background-color: #0d6db9;
        }
        li:hover dl {
            display: block;
        }

        /* 以下是二级菜单下拉动画 */
        /* 有2行时的动画 */
        .items2{
            animation: canvas2 0.3s linear 0s forwards;
        }
        /* 有3行时的动画 */
        .items3{
            animation: canvas3 0.3s linear 0s forwards;
        }
        /* 有4行时的动画 */
        .items4{
            animation: canvas4 0.3s linear 0s forwards;
        }
        /* 有5行时的动画 */
        .items5{
            animation: canvas5 0.3s linear 0s forwards;
        }
        @keyframes canvas2{
            from{
                height: 0px;
            }
            to{
                height: 104px;
            }
        }
        @keyframes canvas3{
            from{
                height: 0px;
            }
            to{
                height: 156px;
            }
        }
        @keyframes canvas4{
            from{
                height: 0px;
            }
            to{
                height: 208px;
            }
        }
        @keyframes canvas5{
            from{
                height: 0px;
            }
            to{
                height: 260px;
            }
        }
    </style>
</head>
<body>
<div class='nav'>
    <ul>
        <li>
            <a href="">网站首页</a>
        </li>
        <li>
            <a href="">学院概况</a>
            <dl class="items5">
                <dd><a href="">学院领导</a></dd>
                <dd><a href="">机构设置</a></dd>
                <dd><a href="">岗位职责</a></dd>
                <dd><a href="">校园风光</a></dd>
                <dd><a href="">联系方式</a></dd>
            </dl>
        </li>
        <li>
            <a href="">招生专栏</a>
            <dl class="items3">
                <dd><a href="">招生简章</a></dd>
                <dd><a href="">学生报名</a></dd>
                <dd><a href="">录取查询</a></dd>
            </dl>
        </li>
        <li>
            <a href="">培训专栏</a>
            <dl class="items4">
                <dd><a href="">培训动态</a></dd>
                <dd><a href="">客房概况</a></dd>
                <dd><a href="">培训设施</a></dd>
                <dd><a href="">客房在线预约</a></dd>
            </dl>
        </li>
        <li>
            <a href="">教学管理</a>
            <dl class="items4">
                <dd><a href="">通知公告</a></dd>
                <dd><a href="">教务管理</a></dd>
                <dd><a href="">考务管理</a></dd>
                <dd><a href="">教材管理</a></dd>
            </dl>
        </li>
        <li>
            <a href="">学籍管理</a>
            <dl class="items3">
                <dd><a href="">通知公告</a></dd>
                <dd><a href="">规章制度</a></dd>
                <dd><a href="">学位管理</a></dd>
            </dl>
        </li>
        <li>
            <a href="">学生管理</a>
            <dl class="items4">
                <dd><a href="">学工队伍</a></dd>
                <dd><a href="">学生组织</a></dd>
                <dd><a href="">学生风采</a></dd>
                <dd><a href="">学生手册</a></dd>
            </dl>
        </li>
        <li>
            <a href="">党建工作</a>
            <dl class="items3">
                <dd><a href="">两学一做</a></dd>
                <dd><a href="">支部建设</a></dd>
                <dd><a href="">党员活动</a></dd>
            </dl>
        </li>
        <li>
            <a href="">工作流程</a>
            <dl class="items2">
                <dd><a href="">服务指南</a></dd>
                <dd><a href="">相关下载</a></dd>
            </dl>
        </li>
    </ul>
</div>
</body>
</html>
```

