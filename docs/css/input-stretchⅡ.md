# 可伸缩input输入框

?> 背景知识：👉[input]()，[blur]()，[focus]()



```html
<!DOCTYPE html>
<html lang='en'>
<head>
    <meta charset='UTF-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-B0vP5xmATw1+K9KRQjQERJvTumQW0nPEzvF6L/Z6nronJ3oUOFUFpCjEUQouq2+l" crossorigin="anonymous">
    <link href="http://netdna.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <title></title>
    <style>
        .focusblurmenu {
            width: 1000px;
            margin: 0 auto;
            overflow: hidden;
            padding: 0px;
            position: relative;
        }

        .focusblurmenu input {
            float: right;
            padding: 0px;
        }

        button {
            position: absolute;
            right: 0px;
            cursor: pointer;
            box-shadow: none;
            background-color: transparent;
            height: 34px;
            line-height: 0.5 !important;
        }

        .focusblurmenu .searchkey {
            width: 225px;
            height: 34px;
            line-height: 34px;
            padding: 6px 12px;
            border: #CCC solid 1px;
            border-radius: 4px;
            background-color: transparent;
        }
        .focusblurmenu .searchbtn {
            padding-left: 0 auto;
            cursor: pointer;
            background-color: #666;
            border: #CCC solid 1px;
            background-color: transparent;
            height: 26px;
            line-height: 26px;
            margin-left: 4px;
        }

        /* 修改input的placeholder样式 */
        input::-webkit-input-placeholder {
            color: #999;
            font-size: 14px;
        }
        input::-moz-placeholder {
            /* Mozilla Firefox 19+ */
            color: #555;
            font-size: 14px;
        }
        input:-moz-placeholder {
            /* Mozilla Firefox 4 to 18 */
            color: #555;
            font-size: 14px;
        }
        input:-ms-input-placeholder {
            /* Internet Explorer 10-11 */
            color: #555;
            font-size: 14px;
        }
        input:focus {
            outline-color: #3b99fc;
            box-shadow: inset 0 1px 1px rgb(0 0 0 / 8%);
        }
    </style>
</head>

<body>
    <form class="focusblurmenu">
        <button class="btn"><i class="fa fa-search"></i></button>
        <input type="text" placeholder="搜索问题或关键字" id="searchkey" class="searchkey">
    </form>
</body>
</script>
<script src="http://lib.sinaapp.com/js/jquery/1.6.2/jquery.min.js" type="text/javascript"></script>
<script>
    $(document).ready(function () {
        //focusblurmenu
        jQuery.focusblurmenu = function (focusdom, focuswidthnew, animatetime) {
            var focusblurmenuid = $(focusdom);
            var defval = focusblurmenuid.val();
            var defwidth = focusblurmenuid.width() + 10; // 发现会丢失10px，所以加回去
            console.log(defwidth)
            focusblurmenuid.focus(function () {
                var thisval = $(this).val();
                if (thisval == defval) {
                    $(this).val("");
                    $(this).animate({
                        width: "+" + focuswidthnew
                    }, focuswidthnew).addClass("searchkeyfocus");
                }
            });
            focusblurmenuid.blur(function () {
                var thisval = $(this).val();
                if (thisval == "") {
                    $(this).val(defval);
                }
                console.log(defwidth);
                $(this).animate({
                    width: "+" + defwidth
                }, focuswidthnew).removeClass("searchkeyfocus");
            });

        };
        $.focusblurmenu(".searchkey", "660px", "100");
    });
</script>

</html>
```

