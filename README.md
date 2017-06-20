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

#### 十一. props属性验证
> 属性验证主要是通过在组件类里面设置静态属性`propTypes`进行控制的

```js
  class Header extends React.Component{
      static propTypes = {
        'props属性的名称': React.PropsTypes['类型验证']
      }
  }
  // 或者
  Header.propTypes = {
    'props属性的名称': React.PropsTypes['类型验证']
  }
```
 > 注意第一种设置静态属性的方式需要安装:`babel-plugin-transform-runtime`和`babel-plugin-transform-class-properties`这两个属性，并在`babel`配置文件或者`webpack.config.js`中指明

#### 十二. props默认值

> 设置props的默认值，主要是使用组件类的静态属性defaultProps

```js
  class Header extends React.Component{
      static defaultProps = {
        'props属性的名称': '默认值'
      }
  }
  // 或者
  Header.defaultProps = {
    'props属性的名称': React.PropsTypes['类型验证']
  }
```

#### 十三. 一个小技巧－－给组件同时传递多个值

```js
  <Header {...Object}/>
  // 如
  <Header {...this.props}/>
```

#### 十四. 获取原生dom元素的方法

1⃣️：通过生js的api结合`ReactDOM.findDOMNode`方法

```js
  const btn = document.getElementById('btn')
  ReactDOM.findDOMNode(btn).style.backgroundColor = 'red'
```

2⃣️：通过`refs`的方法(推荐但是不要滥用)

```js
  <input type="text" ref="btn" />
  // 获取
  this.refs.btn //获取的就是原生元素
```

#### 十五. Mixins

>Mixins主要作用就是在不同的组件下面公用方法

> 如果你想通过es6的方式来书写Mixins需要先安装`react-mixin`

```js
  import ReactMixin from 'react-mixin'
  import Mixins from './Mixins' // 自己定义的文件Mixins文件

  class Header extends React.Component{

  }

  // 使用Mixins  --  Mixins也可以使用生命周期的方法
  ReactMixin(Header.prototype, Mixins)
```

#### 十六. react中使用样式

1⃣️：直接使用js变量定义样式

```js
  const style = {
    header:{
      backgroundColor:'#ccc',
      color:'red',
      "margin-top": "15px",
      paddingBottom: "20px"
    }
  }

  // 使用
  render() {
    return (
      <header style={style.header}></header>
    )
  }
```

2⃣️：引入外部的css

>注意注意注意：在我们给组件中的元素设置`class`的时候，一定一定一定不能使用`class`关键字。应该使用`className`来设置

```html
  <div className="red"></div>
```

3⃣️：内联样式中的表达式:不同的数据使用不同的样式

```js
const style = {
  header:{
    backgroundColor:'#ccc',
    color:'red',
    "margin-top": "15px",
    paddingBottom: (this.state.minHeight) ? '' : '100px'
  }
}
```

4⃣️：css模块化
> 依赖三个插件
