# react 教程

## react 一个UI框架

`React`用于构建用户界面的 `JavaScript` 库.

### react 特点

- mvvm
- 声明式
- 组件化
- 生态强大

## 学习前置基础

- [html\css\js](https://qtxh.ke.qq.com/?tuin=1eb4a0a4)免费视频教程
- [es6+](https://ke.qq.com/course/318503?tuin=1eb4a0a4)
- [webpack教程](https://ke.qq.com/course/321174?tuin=1eb4a0a4)
- [nodejs基础|sass|ajax|...](https://ke.qq.com/course/294595?tuin=1eb4a0a4)

## 快速入门

快速构建一个React的前端项目最好的就是用脚手架快速生成一个项目架构目录，并做好基础的配置。建议使用[`Create React App`](https://github.com/facebook/create-react-app)。

### 安装`Create React App`

```sh
# 建议全局安装
$ npm install -g create-react-app

# yarn
$ yarn global add create-react-app
```

测试是否安装成功：

```sh
$ create-react-app -V
2.1.3
```

### 快速初始化一个react项目

```sh
npx create-react-app myapp
cd myapp
npm start
```

![](https://camo.githubusercontent.com/29765c4a32f03bd01d44edef1cd674225e3c906b/68747470733a2f2f63646e2e7261776769742e636f6d2f66616365626f6f6b2f6372656174652d72656163742d6170702f323762343261632f73637265656e636173742e737667)

此时打开`http://localhost:3000/`就能看到基本的一个简单的web页面。

### 释放webpack的配置文件

由于create-react-app脚手架生成的项目所有的配置都内置在代码中，我们看不到webpack配置的细节，需要通过一个命令，把所有配置都显示的展现在项目中。

```sh
npm run eject
```

> 除非您对webpack已经非常熟悉，请不要这么操作！

### 其他的构建辅助脚本

```sh
# 构建项目
npm run build

yarn build

# 运行测试
npm run test
yarn test

# 另外一种构建方式
# required npm 6.0+
npm init react-app my-app

yarn create react-app my-app

```

## HelloWorld

项目的默认目录：

```sh
├── package.json
├── public                  # 这个是webpack的配置的静态目录
│   ├── favicon.ico
│   ├── index.html          # 默认是单页面应用，这个是最终的html的基础模板
│   └── manifest.json
├── src
│   ├── App.css             # App根组件的css
│   ├── App.js              # App组件代码
│   ├── App.test.js
│   ├── index.css           # 启动文件样式
│   ├── index.js            # 启动的文件（开始执行的入口）！！！！
│   ├── logo.svg
│   └── serviceWorker.js
└── yarn.lock

```

`index.js`就是项目启动启动的入口。

```js
import React from 'react';                           // 引入react核心库（必须）
import ReactDOM from 'react-dom';                    // 引入react在浏览器上运行的需要的支持库
import './index.css';
import App from './App';                             // 引入App组件
import * as serviceWorker from './serviceWorker';    // 注册serviceWork

// 此行代码的意思：把App组件的内容经过Ract的编译生成最终的html挂载到 root的dom节点生。
ReactDOM.render(<App />, document.getElementById('root'));  // !!!核心代码

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: http://bit.ly/CRA-PWA
serviceWorker.unregister();
```

核心代码就是下面一行：把App组件的内容经过Ract的编译生成最终的html挂载到 root的dom节点生。

`ReactDOM.render(<App />, document.getElementById('root'));  // !!!核心代码`

那么我们看一下App组件的代码：

```js
import React, { Component } from 'react';   // 引入react的组件根对象
import logo from './logo.svg';
import './App.css';

class App extends Component {              // 创建App组件类型，继承Component
  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}
export default App;
```

> 您需要有[es6](https://ke.qq.com/course/318503?tuin=1eb4a0a4)的语法的基础。

在App.js中就做了以下几件事：

- 引入React库
- 定义App类型（继承自React.Component)
- 在App类中定义render方法
- 在render方法中返回要渲染的html（jsx语法）

然后我们修改如下App.js为：

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <h1>Hi, aicoder.com</h1>
      </div>
    );
  }
}

export default App;
```

此时页面会自动刷新为：

```sh
Hi, aicoder.com
```

## JSX语法

JSX， 一种 JavaScript 的语法扩展。JSX 用来声明 React 当中的元素。

比如定义一个变量：

```js
// jsx语法是js和html的组合，本质还是js，最终会编译成js
const element = <h1>Hello, world!</h1>;
```

JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。

### JSX中使用表达式

如果JSX中的代码超过一行，我们一般用一个()进行分组处理，遇到html一般都会单独写在一个新行。

```js
const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);
```

再比如：

```js
// 用{}可以直接展示数据内容个，类似es6模板字符串中的 ${}
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {user}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### JSX 属性与{}

你可以使用引号来定义以字符串为值的属性：

```js
const element = <div tabIndex="0"></div>;
```

也可以使用大括号来定义以 JavaScript 表达式为值的属性：

```js
const element = <img src={user.avatarUrl} />;
```

### JSX 防注入攻击

你可以放心地在 JSX 当中使用用户输入：

```js
const title = <span>你好！</span>;
// 直接使用是安全的：
const element = <h1>{title}</h1>;
```

React DOM 在渲染之前默认会 过滤 所有传入的值。它可以确保你的应用不会被注入攻击。所有的内容在渲染之前都被转换成了字符串。这样可以有效地防止 XSS(跨站脚本) 攻击。

### 数组的展示

变量是一个数组，则会展开这个数组的所有成员。

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    var arr = [
      <h1>hi, aicoder.com</h1>,
      <h2>React is awesome</h2>,
    ];
    return (
      <div className="App">
        {arr}
      </div>
    );
  }
}
export default App;
```

最终结果：

```sh
hi, aicoder.com
React is awesome
```

### 数组map输出一个列表

App.js如下：

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    var arr = ['aicoder.com', 'hamkd.com']
    return (
      <div className="App">
        <h1>aicoder.com</h1>
        <ul>
          {
            arr.map((item, index) =>
              <li>{ index +1 } - { item }</li>
            )
          }
        </ul>
      </div>
    );
  }
}
export default App;

```

最终结果：

```sh
aicoder.com
1 - aicoder.com
2 - hamkd.com
```

### JSX的最终归宿

JSX 本质会被编译成JS，Babel 转译器会把 JSX 转换成一个名为 `React.createElement()` 的方法调用。

下面两种代码的作用是完全相同的：

```js
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

```js
React.createElement() 这个方法首先会进行一些避免bug的检查，之后会返回一个类似下面例子的对象：

// 注意: 以下示例是简化过的（不代表在 React 源码中是这样）
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world'
  }
};
```

这样的对象被称为 “React 元素”。它代表所有你在屏幕上看到的东西。React 通过读取这些对象来构建 DOM 并保持数据内容一致。

## React组件

组件可以将UI切分成一些独立的、可复用的部件，这样你就只需专注于构建每一个单独的部件。

组件从概念上看就像是函数，它可以接收任意的输入值（称之为“props”），并返回一个需要在页面上展示的React元素。

### 函数定义/类定义组件

定义一个组件最简单的方式是使用JavaScript函数：

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

该函数是一个有效的React组件，它接收一个单一的“props”对象并返回了一个React元素。我们之所以称这种类型的组件为函数定义组件，是因为从字面上来看，它就是一个JavaScript函数。

你也可以使用 [ES6 class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) 来定义一个组件:

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

上面两个组件在React中是相同的。

### 组件渲染

在前面，我们遇到的React元素都只是DOM标签：

```js
const element = <div />;
```

然而，React元素也可以是用户自定义的组件：

```js
const element = <Welcome name="Sara" />;
```

当React遇到的元素是用户自定义的组件，它会将JSX属性作为单个对象传递给该组件，这个对象称之为“props”。

例如,这段代码会在页面上渲染出"Hello,Sara":

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// ...
class App extends Component {
  render() {
    return (
      <div className="App">
        <Welcome name="Sara" />
      </div>
    );
  }
}
// ...
```

我们来回顾一下在这个例子中发生了什么：

1. 我们对`<Welcome name="Sara" />`元素调用了`ReactDOM.render()`方法。
2. React将`{name: 'Sara'}`作为props传入并调用`Welcome`组件。
3. `Welcome`组件将`<h1>Hello, Sara</h1>`元素作为结果返回。
4. 将DOM更新为`<h1>Hello, Sara</h1>`。

>**警告:**
>
>组件名称必须以大写字母开头。
>
>例如，`<div />` 表示一个DOM标签，但 `<Welcome />` 表示一个组件，并且在使用该组件时你必须定义或引入它。

### 组合组件

组件可以在它的输出中引用其它组件，这就可以让我们用同一组件来抽象出任意层次的细节。在React应用中，按钮、表单、对话框、整个屏幕的内容等，这些通常都被表示为组件。

例如，我们可以创建一个`App`组件，用来多次渲染`Welcome`组件：

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}
```

通常，一个新的React应用程序的顶部是一个`App`组件。但是，如果要将React集成到现有应用程序中，则可以从下而上使用像`Button`这样的小组件作为开始，并逐渐运用到视图层的顶部。

>**警告:**
>
>组件的返回值只能有一个根元素。这也是我们要用一个`<div>`来包裹所有`<Welcome />`元素的原因。

### 提取组件

你可以将组件切分为更小的组件，这没什么好担心的。

例如，来看看这个`Comment`组件：

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

这个组件接收`author`(对象)、`text`(字符串)、以及`date`(Date对象)作为props，用来描述一个社交媒体网站上的评论。

这个组件由于嵌套，变得难以被修改，可复用的部分也难以被复用。所以让我们从这个组件中提取出一些小组件。

首先，我们来提取`Avatar`组件：

```js
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```

`Avatar`作为`Comment`的内部组件，不需要知道是否被渲染。因此我们将`author`改为一个更通用的名字`user`。

我们建议从组件自身的角度来命名props，而不是根据使用组件的上下文命名。

现在我们可以对`Comment`组件做一些小小的调整：

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

提取组件一开始看起来像是一项单调乏味的工作，但是在大型应用中，构建可复用的组件完全是值得的。当你的UI中有一部分重复使用了好几次（比如，`Button`、`Panel`、`Avatar`），或者其自身就足够复杂（比如，`App`、`FeedStory`、`Comment`），类似这些都是抽象成一个可复用组件的绝佳选择，这也是一个比较好的做法。

### Props的只读性

无论是使用[函数或是类](#函数定义/类定义组件)来声明一个组件，它决不能修改它自己的props。来看这个`sum`函数：

```js
function sum(a, b) {
  return a + b;
}
```

类似于上面的这种函数称为[“纯函数”](https://en.wikipedia.org/wiki/Pure_function)，它没有改变它自己的输入值，当传入的值相同时，总是会返回相同的结果。

与之相对的是非纯函数，它会改变它自身的输入值：

```js
function withdraw(account, amount) {
  account.total -= amount;
}
```

React是非常灵活的，但它也有一个严格的规则：

**所有的React组件必须像纯函数那样使用它们的props。**

当然，应用的界面是随时间动态变化的，后面会介绍一种称为“state”的新概念，State可以在不违反上述规则的情况下，根据用户操作、网络响应、或者其他状态变化，使组件动态的响应并改变组件的输出。
