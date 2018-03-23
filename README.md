## 神州云动-前端开发 [React](https://github.com/facebook/react) 编程规范

[基本规则](基本规则)  
[命名](#命名)  
[声明](#声明)  
[对齐](#对齐)  
[引号](#引号)  
[空格](#空格)  
[属性](#属性)  
[括号](#括号)  
[方法](#方法)  
[组件函数](#组件函数)
[顺序](#顺序)  

### 基本规则
* 统一全部采用 [ES6](http://es6.ruanyifeng.com/) 语法
  > React 升级后就支持了 ES6 的class语法，我们可以使用class App extends React.Component{...}的方式创建组件，这也是目前官方推荐创建有状态组件的方式。
* 每个文件 `只包含一个React组件`
* 使用 `JSX` 语法
* 除非是从一个非 `JSX` 文件中初始化 app，否则不要使用React.createElement

> `Class` vs `React.createClass`  
   除非有更好的理由使用 `混淆(mixins)` 否则就使用组件继承 `React.Component`。eslint 规则：[react/prefer-es6-class](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-es6-class.md)  


``` javascript
// 正确方式
import { Component } from 'react'
class App extends Component {
  return() {
    return <div />;
  }
};

// 错误方式
const App = React.createClass({
  render() {
    return <div />;
  }
});
```  

### 命名
* 扩展名：使用 `JSX` 作为React组件的扩展名
* 文件名：文件命名采用 [帕斯卡命名法](https://baike.baidu.com/item/%E5%B8%95%E6%96%AF%E5%8D%A1%E5%91%BD%E5%90%8D%E6%B3%95/9464494?fr=aladdin)，如：`FileName.jsx`
* 引用名：组件引用采用帕斯卡命名法，其实参照采用 [驼峰是命名法](https://baike.baidu.com/item/%E9%A9%BC%E5%B3%B0%E5%BC%8F%E5%A4%A7%E5%B0%8F%E5%86%99/3976226?fr=aladdin)。eslint rules：[react/jsx-pascal-case](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)    

``` javascript
  // 正确方式
  import FileName from './FileName';

  // 错误方式  
  import fileName from './FileName';

  // 正确方式
  const fileName = <Component />;

  // 错误方式
  const FileName = <Component />;
```  

* 组件命名：使用文件名作为组件名。例如：`MainContainer.jsx` 组件的引用名应该是 `MainContainer` 。然而，对于一个目录的根组件，应该使用 `index.jsx` 作为文件名，使用目录名作为组件名。  

``` javascript
  // 正确方式
  import MainCOntainer from './Main';

  // 错误方式
  import MainContainer from './Main/MainContainer.jsx';

  // 错误方式
  import MainContainer from './Main/index.jsx';
```  


* 变量命名：为了增强程序的可读性，需要在变量名前加入代表其实际数据类型的前缀。例如：strUserName，intPageSize等。

### 声明
* 不要通过 `displayName` 来命名组件，通过引用来命名组件。  

``` javascript
  // 正确方式
  import React, { Component } from 'react';
  export default class MainContainer extends Component{
    // code...
  };

  // 正确方式 
  import React, { Component } from 'react';
  class MainContainer extends Component{
    // code...
  };
  export default MainContainer;

  // 错误方式
  export default React.createClass({
    displayName : 'MainContainer',
    // code goes here
  })
```  

### 对齐
* 对于 `JSX` 语法，遵循下面的对齐风格。 eslint rules： [react/jsx-closing-bracket-location](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)  

``` javascript
  // 正确方式
  <MainContainer 
    userName="吴磊"
    userAge="25"
  />

  // 如果只有一个props，保持一行即可
  <MainContainer userName="吴磊" />

  // 子组件正常缩进
  <MainContainer 
    userName="吴磊"
    userAge="25"
  >
    <MainBody />
  </MainContainer>

  // 错误方式
  <MainContainer userName="吴磊"
                 userAge="25"/>
```

### 引号
* 对于 `JSX` 使用双引号，对其他所有 `JS` 属性使用单引号  
> 为什么？因为 `JSX` 属性不能包含被转移的引号，并且双引号使得如 `"don't"` 一样的连接词很容易被输入。常规的HTML属性也应该使用双引号而不是单引号，`JSX` 属性反应了这个约定。  

eslint rules：[jsx-quotes]()  
``` javascript
  // 正确方式
  <MainContainer userName="吴磊" />

  // 错误方式
  <MainContainer userName='吴磊' />

  // 正确方式
  <MainContainer style={{ left : '20px'}} />

  // 错误方式
  <MainContainer style={{ left : "20px"}} />
```

### 空格  
* 在自闭和标签之前，留一个空格  

```javascript  
  // 正确方式
  <MainContainer />

  // 错误方式 
  <MainContainer/>

  // 错误方式
  <MainContainer
    />
```  

### 属性  

* 属性名采用驼峰式命名法  

``` javascript  
  // 正确方式
  <MainContainer
    userName="吴磊"
    userAge="25"
  />

  // 错误方式
  <MainContainer
    UserName="吴磊"
    user_age="25"
  />
```

### 括号  
* 当组件跨行时，要用括号包裹 JSX 标签。eslint rules：[react/wrap-multilines]()  

``` javascript  
  // 正确方式
  render() {
    return (
      <MainContainer className="body main" userName="吴磊">
        <MainBody />
      </MainContainer>
    )
  };

  // 正确方式
  render() {
    const body = <div>hello</div>;
    return <MainContainer>{body}</MainContainer>
  };

  // 错误方式
  render() {
    return <MainContainer className="body main" userName="吴磊">
             <MainBody />
           </MainContainer>
  };
```

### 标签  
* 没有子组件的父组件使用自闭和。eslint rules：[react/self-closing-comp](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)  

``` javascript
  // 正确方式
  <MainContainer className="main body" />

  // 错误方式
  <MainContainer></MainContainer>
```
* 如果组件有多行属性，闭合标签应写在新的一行上。eslint rules：[react/jsx-closing-bracket-location](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)  

``` javascript
  // 正确方式
  <MainContainer 
    userName="吴磊"
    userAge="25" 
  />

  // 错误方式
  <MainContainer 
    userName="吴磊"
    userAge="25" />
```

### 方法
* 不要针对 React 组件的内置方法使用 `underscore` 前缀。  

``` javascript
  // 正确方式 
  class App extends Component {
    onClickSubmit() {
      // code...
    }
  }

  // 错误方式
  React.createClass({
    _onClickSubmit() {
      // code...
    }
  })
```

### 组件函数  
* ES5写法 `React.createClass`;
* ES6写法 `React.Component`;
* 无状态的函数式写法[(纯组件-SFC)](http://www.jianshu.com/p/9ea8df92b2ac)  

> ES5写法-不推荐  

``` javascript
  var React = require('react');
  var ReactDOM = require('react-dom');
  var App = React.createClass({
    getDefaultProp:function() {
      // code...
    },

    getInitialState: function() {
      // code...
    },

    handleClick: function(event) {
      // code...
    },

    render: function() {
      return (
        <div>
          <MainCOntainer userName="吴磊" />
        </div>
      );
    }
  });
```

> ES6写法-有状态组件可以用  

``` javascript

  import React,{ Component } from 'react'
  import { render } from 'react-dom'
  class App extends React.Component {
      constructor(props) {
        super(props)
        this.state = {
          // code...
        }
      }
    
      render() {
        return (
          <div>
            <MainCOntainer userName="吴磊" />
          </div>
        )
      }
  }
```

> 无状态的函数式写法-纯组件SFC，推荐  

``` javascript
  // 函数式的方式声明
  import React,{ Component } from 'react'
  import { render } from 'react-dom'
  class App extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        // code...
      }
    }

    render() {
      return (
        <div>
          <MainContainer 
            userName="吴磊" 
            id="38UY37WYu371"
          />
        </div>
      )
    }
  }

  const MainContainer = (props) => {
    <div data-id={props.id}>
      {props.userName}
    </div>
  }


  // 对于props为 Object 类型时，我们还可以使用 ES6 的解构赋值
  import React,{ Component } from 'react'
  import { render } from 'react-dom'
  class App extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        // code...
      }
    }

    render() {
      return (
        <div>
          <MainContainer 
            userName="吴磊" 
            id="38UY37WYu371"
            userAge="25"
            height="180"
          />
        </div>
      )
    }
  }

  const MainContainer = ({ userName,id,...props}) => {
    <div 
      data-id={id}
      {...props}
    >
      {props.userName}
    </div>
  }
```


### 顺序
* 继承 `React.Component` 的类方法遵循下面的顺序
1. constructor
1. optional static methods
1. getChildContext
1. componentWillMount
1. componentDidMount
1. componentWillReceiveProps
1. shouldComponentUpdate
1. componentWillUpdate
1. componentDidUpdate
1. componentWillUnmount
1. clickHandlers or eventHandlers like onClickSubmit() or onChangeDescription()
1. getter methods for render like getSelectReason() or getFooterContent()
1. Optional render methods like renderNavigation() or renderProfilePicture()
1. render

* 怎么定义propTypes，defaultProps，contextTypes等等...  

``` javascript
  import React, { Component,PropTypes } from 'react';

  const propTypes = {
    id : PropTypes.number.isRequired,
    url : PropTypes.string.isRequired,
    text : PropTypes.string
  };

  const defaultProps = {
    text : 'Hello Word'
  };

  class App extends Component {
    static methodsAreOk(){
      return true;
    }
  };

  render() {
    return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>
  };

  App.propTypes = propTypes;
  App.defaultProps = defaultProps;

  export default App;
```
