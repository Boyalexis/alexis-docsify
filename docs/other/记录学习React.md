# 记录学习React

## React是什么

React是一个简单的javascript UI库，用于构建高效、快速的用户界面。

## React的特点

* 声明式写法

  你只需要描述UI（HTML）看起来是什么样，就跟写HTML一样，React负责将你写的HTML渲染出来

* 组件化

  React 中一切都是组件（万物皆可组件）。 我们通常将应用程序的整个逻辑分解为小的单个部分。 我们将每个单独的部分称为组件。 通常，组件是一个javascript函数，它接受输入，处理它并返回在UI中呈现的React元素。 

## 配置React开发环境

构建一个react项目

```bash
npx create-react-app my-project		// my-project为自己的项目名
```

### npx是什么？

npm 从5.2版开始，增加了 npx 命令。那么npx有什么用呢？

* 避免安装全局模块

  npx将create-react-app下载到一个临时目录，使用完后删除。比如，`create-react-app`这个模块是全局安装，npx 可以运行它，而且不进行全局安装。

* 调用项目内部安装的模块

举个例子：

```bash
npm install mocha -D      //全局安装mocha模块

//一般来说，如果要调用mocha，必须像下面这样

node_modules/.bin/mocha -v
```

而使用npx，就解决了这个繁琐的问题：

```bash
npx create-react-app my-react-app    //非全局安装

npx webpack -v 
```

构建完项目后启动

```bash
npm start
```

## 项目文件结构

​	在[React官方文档](https://react.docschina.org/docs/faq-structure.html)中对项目文件结构没有要求，不过它推荐了两种组织项目文件结构的方式：1.按功能或路由组织 2.按文件类型组织

```javascript
// 按文件类型组织
api/
  APIUtils.js
  APIUtils.test.js
  ProfileAPI.js
  UserAPI.js
components/
  Avatar.js
  Avatar.css
  Feed.js
  Feed.css
  FeedStory.js
  FeedStory.test.js
  Profile.js
  ProfileHeader.js
  ProfileHeader.css
```

​	我个人比较喜欢第二种按文件类型组织的方式，这样的项目结构看起来简洁大方，一目了然

### 避免多层嵌套！！

在这里React官网特意提到了避免文件结构多层嵌套的问题。我之前也这样做过，看起来很高(wu)级(liao)把每一个文件都分好区，但是这样一来本来功能并不复杂的项目却人为增加了复杂度，看起来很繁琐，引入也很麻烦

### 文件名命名方式

推荐使用[帕斯卡命名法](https://baike.baidu.com/item/%E5%B8%95%E6%96%AF%E5%8D%A1%E5%91%BD%E5%90%8D%E6%B3%95/9464494?fr=aladdin)，即**命名中每个单词的首字母大写**，例如`FileList.js`、`FileItem.js`

## React Hooks

### useState Hook

```javascript
const [ state, setState ] = useState(0)
```

useState接收一个初始值，返回的是一个数组，第一项是当前的state，第二项是更新state的函数。例如，useState(0)中的0是state的初始值。

useState不仅可以接收一个初始值，也可以接收一个函数`action`，`action`返回值作为新的state，例如：

```javascript
const [ time, setTime ] = useState(new Date())
```

`setState` 函数用于更新 state，它接收一个新的 state 值并将组件的一次重新渲染加入队列。

### useEffect Hook

useEffect通常用来作为函数组件的生命周期函数，useEffect接收两个参数，第一个参数是当依赖`dep`更新时执行的函数，第二个参数是需要监听的依赖`dep`

**如果不传入第二个参数则所有更新都执行。如果传入空数组那么仅在页面挂载和卸载时执行**

```javascript
useEffect(() => {
    console.log('useEffect')
})	// 所有更新都执行
```

```javascript
useEffect(() => {
    consoe.log('useEffect')
},[]) // 仅在页面渲染和更新时执行
```

```javascript
useEffect(() => {
    console.log('useEffect')
},[like])	// 仅在like更新时执行
```

注意：如果在useEffect内返回一个函数，那么React就在执行清除时操作它

### 自定义hook

注意：自定义hook的函数名需要以`use`开头

### 类组件  Or  函数组件？

```javascript
// 类组件
class Welcome extends React.Component {
  constructor(props) {
      super(props);
      this.sayHi = this.sayHi.bind(this);
  }
  sayHi() {
      alert(`Hi${props.name}`);
  }
  render() {
    return (
      <h1>Hi, {this.props.name}</h1>
      <button onClick={this.sayHi}>Say Hi</button>
    );
  }
}
```

```javascript
// 函数组件
function Welcome(props) {
    const sayHi = () => alert(`Hi,${props.name	}`)
    return (
    	<h1>Hi,{props.name}</h1>
        <button onClick={sayHi}>Say Hi</button>
    )
}
```

**两者的区别：**

1. 函数组件中，没有`this`，没有状态`State`，也无法使用组件的生命周期方法，而这些在类组件中都有

   btw：在函数组件中使用`useState`改变state，用`useEffect`弥补函数组件没有生命周期的缺点，而在类组件中使用`this.setState`改变state状态，并且可以使用`componentDidMount`等生命周期函数，

2. 由于类组件需要实例化而函数组件不用，函数组件的性能比类组件性能要高

### 组件间的通信

props

### HOC(Higher order component)高阶组件

高阶组件就是一个函数，接收一个组件作为参数，返回一个新组件

那么HOC有什么用呢？

* 抽取重复代码，实现组件复用

* HOC可以通过组件嵌套的方法给子组件添加更多功能，

注意：自定义HOC高阶组件的命名一般都由`with`开头

## React-Router

react-router 是一个基于 [React](http://facebook.github.io/react/) 之上的强大路由库，它可以让你向应用中快速地添加视图和数据流，同时保持页面与 URL 间的同步。

​	传统网站的路由方式是根据用户访问的不同的url，浏览器从服务器获取对应页面的内容展示给用户。这样造成服务器压力比较大，而且用户访问速度也比较慢，并且由于网站的url与服务器文件结构是一一对应的，这种配置方案会直接暴露服务器文件夹结构，在这种场景下，出现了**单页应用SPA**。

**SPA**：Single Page Application 单页应用

浏览器一开始会加载必需的HTML、CSS和JavaScript，所有的操作都在这张页面上完成，都由JavaScript来控制。JavaScript劫持浏览器路由，生成虚拟路由来动态渲染页面DOM元素

​	随着React、Vue、Angular前后端分离技术的兴起，网站的路由架构彻底改变，url地址与真实的服务器文件结构不再一一对应，而是通过某种特定的算法映射起来。现代网站的路由方式一般浏览器向前端请求页面资源，向后端请求数据资源。前端提供SPA文件，由SPA劫持浏览器路由从而控制页面之间的切换，而后端只需要访问数据库取得数据返回给浏览器，由UI渲染数据

### 安装react-router

```bash
npm install react-router-dom
或 yarn add react-router-dom
```

为什么这里是react-router-dom而不是react-router呢？react-router是整个路由的核心，它提供了路由最基本的功能，但实际上我们在使用时不会直接使用reacxt-router的功能，而是根据你所开发的程序选择相对应的环境开发组件。比如说我们项目的网站应用，那么我们就需要用到react-router-dom，如果我们使用ReactNative开发手机应用处理路由，那么我们就需要用到react-router-native。而让我们安装react-router-dom的时候，会自动安装react-router核心框架

<Link />组件可以渲染出<a />标签

<BrowserRouter />组件可以利用H5 API实现路由切换

<HashRouter />组件则利用原生JS中的window.location.hash来实现路由切换

安装好react-router后开始简单的使用：

```javascript
// App.js
import React from 'react';
import { BrowserRouter, Route} from 'react-router'
import { Home, Login } from './pages'

function App() {
    <div className="app">
        <BrowserRouter>
        	<Route exact path="/" component={Home} />
            <Route path="/login" component={Login} />
        </BrowserRouter>
    </div>
}
```

Route组件中的`exact`属性是严格匹配，否则会匹配所有匹配到的路由组价。如果不加exact的话，进入'/login'页时会渲染匹配到的两个组件Home和Login，因为'/login'和'/'都包含了`/`。`path`属性是路径。`component`属性则是该路径下需要渲染的组件。

### Switch

思考下面这个例子，如果进入 '/about' 页会显示什么？

```javascript
function App() {
    <div className="app">
        <BrowserRouter>
        		<Route path="/about" component={About} />
            	<Route path="/:user" component={User} />
        </BrowserRouter>
    </div>
}
```

我们进入`'/about'`时，路由会同时匹配到`'/about'`和`'/:user'`，页面会渲染About组件和User组件，出现页面叠加的情况，exact治标不治本。为了更好的匹配规则，这时候需要用到另一个组件`Switch`。**Swithc组件只显示匹配到的第一个路由**，例如进入`/about`时只渲染`About组件`，进入`/admin`页面时只渲染`User组件`

```javascript
function App() {
    <div className="app">
        <BrowserRouter>
        	<Switch>
        		<Route exact path="/" component={Home} />
            	<Route path="/login" component={Login} />
                <Route path="/about" component={About} />
            	<Route path="/:user" component={User} />
        	</Switch>
        </BrowserRouter>
    </div>
}
```

## React哲学

​	React哲学很好的讲述了我们在开发的时候如何将设计稿拆分为组件，思考在react应用中state应该放在什么位置，这又利于优化项目的性能和可维护性

* 将设计好的UI划分为组件层级，这也是react推崇的理念 --- 万物皆是组件

  例如将掘金首页划分为

  ​	`Header`：顶部logo、菜单、搜索框，通知以及用户头像

  ​	`Navbar`：顶部导航栏，包含推荐、后端、前端...

  ​	`Sortbar`：筛选栏，包含最新，热门，历史

  ​	`ArticleList`：文章列表，子组件为`ArticleItem`

* 创建应用的静态版本

  官方建议：首先用已有的数据渲染一个不包含交互功能的UI，将UI和交互分离开

* 确定UI state的最小表示

  找出组件需要的state，这些state不经由props传入且无法由其他数据计算得来

* 确定state放置的位置

  由于react的单向数据流，我们需要清楚哪个组件应该拥有哪个state

* 添加反向数据流

  在深层级组件更新上层组件的state，由于 state 只能**由拥有它们的组件**进行更改，所以我们只能通过callback调用父组件的setState修改state状态

## 推荐阅读

1. [React函数组件和类组件的差异](https://zhuanlan.zhihu.com/p/62767474)
2. [「React进阶」 React全部api解读+基础实践大全(夯实基础2万字总结)](https://juejin.cn/post/6950063294270930980)
3. [「react进阶」一文吃透React高阶组件(HOC)](https://juejin.cn/post/6940422320427106335)
4. [React哲学](https://react.docschina.org/docs/thinking-in-react.html)