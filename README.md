## React.js

##### 一. react的管理方式
    直接下载引入至源文件
    npm管理(推荐)

##### 二. 安装相关包

```bash
yarn add babel-preset-react babelify react react-dom babel-preset-es2015
```

##### 三. webpack的热加载配置

##### 四. react组建的基本写法
```js
    import React from 'react'
    import ReactDOM from 'react-dom'

    export default class 组件名称 extends React.Component{
        // 组件的基本定义
    }
```
##### 五. 几个需要注意的点

    1⃣️：组件是`react`的一个主要的特性

    2⃣️：组件对于模块化开发的重要性

    3⃣️：组件的`render`方法中`return`的根节点必须是一个

    4⃣️：需要对外引用的组件必须向外暴露

    5⃣️：组件入口定义的一般形式为

```js
   ReactDOM.render(<Index />, document.getElementById('app'))
```

##### 六. `jsx`内置表达式

    1⃣️：三元表达式的使用
```js
    {window.userName == ... ? '' : ''}
```
    2⃣️：布尔值属性的使用
```html
    <input type="button" value="..." disabled={布尔属性变量}/>
```
    3⃣️：{/\*注释\*/}

    4⃣️：设置`innerHtml`
```html
    <div dangerouslySetInner={{__html: 'html的内容'}}></div>
```

##### 七. `react`组件的生命周期

    [组件的生命周期](https://segmentfault.com/a/1190000004168886)

##### 八. `state`属性

    state属性－－－>virtual Dom--->DOM

    1⃣️：`state`的初始化可以放在`constructor中`
```js
    constructor() {
        super()
        this.state = {}
    }
```
    2⃣️：`state`的值只对当前组件其作用

    3⃣️：更改`state`只能使用`this.setState({})`的值
```js
    this.setState({

    })
```

    4⃣️：没有被事先放入`state`的值，也可以实时更新

    5⃣️：`state`的使用

```html
    //在组件中使用
    <div class={this.state.名称}></div>
```


##### 九. `props`属性

    1⃣️：`props`是父组件通过属性的形式传递给子组件的
```html
    <Header userId={123456}/>
```
    2⃣️：子组件中通过`this.props.userId`来获取`props`中的属性值
```html
    <div>{this.props.userId}</div>
```   
    3⃣：`props`的属性对组件自身来说是属于外来属性，和`state`相反

##### 十. 双向绑定

    1⃣️：组件中添加事件处理器一定要使用`bind` 更改`this`
```html
    <div onClick={this.changeUserInfo.bind(this)}></div>
```

    2⃣️：子组件传递数据给父组件，只能通过事件的方式进行处理。基本的方式就是：在父组件中定义好事件监听器，通过`props`传递给自组件，子组件在需要监听的地方进行处理。有一点需要注意的就是，这个时候的`bind`应该绑定到父组件的方法中

```html
    <!--父组件-->
    <!--父组件中的handleMethod第一个参数就是子组件对应的事件对象,同时也可以通过这种方式向父组件传递额外的参数this.handleMethod.bind(this, ...args)-->
    <Index handleMethod={this.handleMethod.bind(this)}></div>
    <!--子组件-->
    <Header onClick={this.props.handleMethod}/>
```
