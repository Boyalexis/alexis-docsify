# electron学习笔记

## **electron**

Electron是一个使用 JavaScript、HTML 和 CSS 构建桌面应用程序的框架，它的出现让前端工程师能够用JavaScript写出跨平台的桌面应用，它几乎是前端开发人员开发桌面客户端的唯一途径，最重要的是，我们可以利用我们学的Vue和React框架构建electron程序，因此学习electron需要我们抱有对技术的热爱。第一次接触electron是在b站的一位up主直播写代码看起来好玩于是学了，最近做在线记账系统的时候想到可以结合electron做一个桌面记账应用，还是挺有意思的。

## **构建electron项目**

方法一：克隆官网的示例项目

```
git clone https://github.com/electron/electron-quick-start

cd electron-quick-start

npm install && npm start
```

方法二：在你的react或vue项目中引入electron

```
# 在项目文件夹下

npm install electron --save-dev
```

然后在项目文件夹中新建`main.js`，添加以下内容

```
// main.js 这个是electron的主进程文件

const { app, BrowserWindow } = require('electron')

let mainWindow;



app.on('ready', () => {

    mainWindow = new BrowserWindow({

        height: 680,

        width: 1024,

    })   // 创建一个高680宽1024的窗口

    mainWindow.loadURL("http://localhost:3000") // React项目对应3000端口，vue项目对应8080端口

})
```

```
// 在package.json

// 加入以下代码

"main": "main.js"
```

然后打开两个cmd窗口进入项目文件夹，在其中一个输入npm start启动react项目，另一个输入`electron .`启动electron

方法三：创建vue-electron项目

```
vue init simulatedgreg/electron-vue project
```

然后cmd会出现项目明细和模块选择，选择需要的模块输入y回车即可

## **主进程与渲染进程**

### **主进程**

Electron运行package.json的main脚本的进程成为主进程，每个应用只有一个主进程，主进程主要用于：

-   管理原生GUI，典型的窗口（**BrowserWindow**、Tray、Dock、Menu）

<!---->

-   创建**渲染进程**

<!---->

-   控制应用生命周期（app）

### **渲染进程**

-   展示Web页面的进程成为渲染进程

<!---->

-   通过Node.js\Electron提供的API可以跟系统底层打交道

<!---->

-   一个Electron应用可以有多个渲染进程

在Electron中开发大体和我们平常开发Web页面一样，但是在普通浏览器中，Web页面是运行在沙盒环境中，无法访问操作系统的原生资源，而Electron可以让我们使用Node.js访问系统底层

## **进程间的通信**

进程间通信的目的主要有三个：

1.  通知事件。比如我们在页面中想创建一个原生菜单，但只有主进程才能够创建原生菜单，因此只能通过IPC进程通信让主进程帮我们创建菜单
1.  数据传输。比如我想在某个页面里获得电脑的内存情况，也是需要IPC进程通信传输
1.  共享数据。比如用户信息在各个进程中都会用到，这时候就需要IPC通信完成数据的共享

## **IPC通信模块**

Electron提供了IPC通信模块，分别是主进程的**ipcMain**和渲染进程的**ipcRenderer**。ipcMain和ipcRenderer都是EventEmitter对象。

进程间通信有几个经典的模型：

### **从渲染进程到主进程**

```
// CallBack写法

ipcRenderer.send(channel, ...args)

ipcMain.on(channel, hanlder)



// Promise写法(Electron7.0之后，处理请求+响应模式)

ipcRenderer.invoke(channel, ...args)

ipcMain.handle(channel, handler)
```

举个栗子：

```
// renderer.js

const { ipcRenderer } = require('electron')



ipcRenderer.send('do-some-work')



// main.js

ipcMain.on('do-some-work', function() {

    console.log('do-some-work')

})
```

这里我们在渲染进程中向主进程发送了do-some-work的请求，在控制台输入npx electron main.js启动后可以发现，控制台打印了`do-some-work`，所以我们ipcRenderer的事件成功发送到我们的主进程

### **从主进程到渲染进程**

思考一下，如果我们用`ipcMain.send`的话会出现什么问题？我们只有一个主进程，但是有多个渲染进程，如果用ipcMain.send的话，**到底发给哪个渲染进程呢**？

我们需要找到一个具体的窗体内容(webContents)，我们可以通过`webContents.send`方法去发送事件给渲染进程

举个栗子：

```
// renderer.js

const { ipcRenderer } = require('electron')



ipcRenderer.on('do-some-render-work', () => {

    alert('do-some-work')

})

// main.js

win.webContents.send('do-some-render-work')
```

### **渲染进程与渲染进程之间的通信**

-   通知事件

    -   通过主进程转发(Electron 5之前)

<!---->

-   ipcRenderer.sendTo(Electron 5之后)

<!---->

-   数据共享

    -   Web技术(localStorage、sessionStorage、indexedDB)

<!---->

-   使用remote

注意：

1.  在开发中要少用尽量不用remote模块，因为每次remote会触发底层的同步IPC事件，会造成程序卡顿，影响性能
1.  千万不要使用sync模式，一旦写的不好整个应用都会卡死
1.  在请求+响应的通信模式下，需要自定义超时限制

好了，以上只是个人学习electron时记录的一点笔记，以后应该还会更新，虽然electron不太火，没什么人做这个玩意儿，但是不得不说，electron还是挺好玩的，强烈推荐大家学这个东西，可以跟着做个番茄钟或者音乐播放器什么的玩一玩，而且技多不压身，多学一门技术，面试的时候就更有底气和面试官掰掰手腕了[doge]