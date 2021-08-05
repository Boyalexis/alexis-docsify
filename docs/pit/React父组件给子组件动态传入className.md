---
title: React父组件给子组件动态传入className
author: alexis
top: false
cover: false
toc: true
mathjax: false
date: 2021-02-3 15:06:59
img:
coverImg:
password:
summary:
tags:
- 前端
- React
categories:
- 前端
- React
---

## React 调用子组件动态传入className

子组件（底部button，需要动态传入的class）：

```javascript
import React from 'react';
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'

const BottomBtn = ({ text, colorClass, icon, onBtnClick }) => {
    return (
        <button
         type="button"
         className={'btn btn-block no-border ' + colorClass}
         onClick={onBtnClick}
        >
          <FontAwesomeIcon
           className="mr-2"
           size="lg"
           icon={icon}
          />
          {text}  
        </button> 
    )
}
export default BottomBtn
```

写法，colorClass为需要传入的class：

```javascript
className={'btn btn-block no-border ' + colorClass}
```

调用组件时传入，这里使用的是bootstrap样式：

```html
<div className="col">
   <BottomBtn
     text="新建"
     colorClass="btn-primary"
     icon={faPlus}
   />
</div>
<div className="col">
   <BottomBtn
     text="导入"
     colorClass="btn-success"
     icon={faFileImport}
   />
</div>
```

#### 踩坑记录：

错误写法：

```javascript
1. className={'btn btn-block no-border ${colorClass}'}
2. className='btn btn-block no-border' + {colorClass}
```

