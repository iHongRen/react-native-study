## React Native 开发规范  

> 保持项目代码的整洁、易读、和一致性，更容易被理解和维护。

(date: 2018-09-16) 持续更新中...



### 基本要求

---

- 代码缩进使用**2**个空格

- 语句结尾必须加分号"**;**"

- 变量声明使用(**const > let > var**)

- 驼峰命名(**camelCase**) & 帕斯卡命名(**PascalCase**)

- 全面使用**[ES6+](http://es6.ruanyifeng.com/)**语法

- 库(升级、添加、删除)、改他人代码前，需进行沟通


### 目录组织结构(不含Redux)

---

```c
AwesomeProject 
.
├── app
│   ├── App.js
│   ├── app.json
│   ├── assets                 //资源(图片、字体)
│   ├── common			      //公共(样式)
│   ├── components		      //可复用的组件（非完整页面）
│   │   └── CommentView
│   ├── config			     //配置项（常量、接口地址、路由、多语言化等预置数据）
│   ├── pages			     //完整页面
│   │   └── HomePage
│   ├── third-party		      //第三方
│   └── utils			     //工具类（非UI组件)
├── index.js
├── android
├── ios
├── node_modules
└── package.json
           
```



### 代码缩进

---

##### 横向：主要考虑空格、换行、每行不超过120个字符

- 代码缩进使用2个空格

  ```jsx
  //不推荐
  export default class App extends React.Component {
      render() {
          return (
              <View />  
          );
      }
  }
  
  //推荐
  export default class App extends React.Component {
    render() {
      return (
        <View />  
      );
    }
  }
  ```

- 方法名、小括号、大括号之间的空格和换行

  ```javascript
  //不推荐
  add () {
  }
  
  add(){
  }
  
  add()
  {
  }
  
  //推荐
  add() {
  }
  ```

- 使用空格把运算符隔开( i++ 除外)

  ```js
  //不推荐
  const x=y+1;
  isOpen?1:0;
  i ++;
  
  //推荐
  const x = y + 1;
  isOpen ? 1 : 0;
  i++
  ```

- 使用模块时，一行显示不下时对所有换行，可以名字长度顺序排序

  ```js
  //不推荐
  import {View} from 'react-native';
  
  import {
    View,
  } from 'react-native';
  
  import { Text, View, StyleSheet, Clipboard, TouchableOpacity, Image } from 'react-native';
  
  //推荐
  import { View } from 'react-native';
  
  import {
    Text,
    View,
    Image,
    Clipboard,
    StyleSheet,
    TouchableOpacity
  } from 'react-native';
  ```


##### 纵向：主要考虑紧密相关的代码相互靠近，自上而下的展示调用依赖顺序 (组件不超过500行，方法不超过40行)

- 文件头顺序：

  ```js
  1.先导react和react-native包里面的组件
  2.导入第三方组件库
  3.导入团队内部的组件库
  4.导入相对路径的文件
  5.const常量
  6.let变量
  
  import React, {Component} from 'react';
  import { StyleSheet } from 'react-native';
  import {} from 'ajd-mobile';
  import ReactWeb from 'react-native-web';
  import DemoPage from './DemoPage';
  const OrderType = 1;
  let name ='value';
  ```

- 组件内的代码顺序为：(方法之间要加一个空白行)

```js
1. propTypes定义 (组件外)
2. static方法
3. constructor
4. 组件生命周期方法
5. render方法
6. 事件处理方法，比如onClickSubmit()、onChangeDescription()
7. 自定义方法

 //propTypes
const propTypes = {    
    sampleProp: PropTypes.bool.isRequired; // 属性描述
};

const defaultProps = {
    name: 'xxx',
};

class LearnReactNative extends Component {
  
  //如果需要定义static方法，放在这里
  static getSampleProp(): boolean {
    return true;
  };   
  
  //constructor方法，里面要初始化state
  constructor(props) {
    super(props);
    this.state = {
      sampleState: this.props.sampleProp
    };
  }
   
  //生命周期方法（按需添加）
  componentWillMount() {}

  componentDidMount() {}

  componentWillReceiveProps() {}

  shouldComponentUpdate() {}

  componentWillUpdate() {}

  componentDidUpdate() {}

  //render方法
  renderItem () {
	return <View />;	
  }

  render() {
    if(this.state.sampleState) {
      return <Text>This is the sample component</Text>
    } else {
      return this.renderItem();
    }
  }
  
  //事件处理方法
  onClickSubmit() {
  }

  //自定义方法
  fetchForumList() {    
  }

}

//样式
const styles = StyleSheet.create({
  xx: {
  }
}) 

//属性定义
LearnReactNative.propTypes = propTypes;
LearnReactNative.defaultProps = defaultProps;
```

##### JSX

```jsx
//对于没有子组件的JSX标签，始终自闭合
//不推荐
<Foo className={stuff}></Foo>

//推荐
<Foo className={stuff} />


//如果组件有多行属性，则另起一行进行自闭合
//不推荐
<Foo name={x}
     content={y} />

//推荐
<Foo
  name={x}
  content={y}
/>

//如果一行能摆下props，那就摆在一行
<Foo name={x} content={y} />

//子组件照常缩进
<Foo
  name={x}
  content={y}
  onPress={z}  
>
  <Sub />
</Foo>
```

 

### 命名规范

---

- 避免使用单字母的名字来描述功能：

  ```js
  //不推荐
  function q() {
    // ...
  }
  
  //推荐
  function query() {
    // ...
  }
  ```

- 在命名对象、函数和实例时使用驼峰命名法（camelCase）：

  ```js
  //不推荐
  const OBJEcttsssss = {};
  const this_is_my_object = {};
  function c() {}
  
  //推荐
  const thisIsMyObject = {};
  function thisIsMyFunction() {}
  ```

- 在命名构造器、类、全局常量的时候用帕斯卡命名法（PascalCase）：

  ```js
  //不推荐
  function user(options) {
    this.name = options.name;
  }
  
  const bad = new user({
    name: 'nope',
  });
  
  //推荐
  class User {
    constructor(options) {
      this.name = options.name;
    }
  }
  
  const good = new User({
    name: 'yup',
  });
  
  //不推荐, 相信很多人对于纯大写的长字符都会有一点恐惧感，
  //不先转为小写就不认识了，所以推荐直接用帕斯卡命名法。
  const CUSTOMER_CALLBACK = 'api/CustomerCallback';
  const ORDER_TYPE = {
    NONE: 0
  };
  
  //推荐
  const CustomerCallback = 'api/CustomerCallback';
  const OrderType = {
    None: 0
  };
  ```

- 不要使用前置或者后置下划线：

  ```js
  //不推荐
  this.__firstName__ = 'Panda';
  this.firstName_ = 'Panda';
  this._firstName = 'Panda';
  
  //推荐
  this.firstName = 'Panda';
  ```

- 文件名应该和默认导出的名称完全匹配：

  ```js
  // file 1 contents
  class CheckBox {
    // ...
  }
  export default CheckBox;
  
  // file 2 contents
  export default function fortyTwo() { return 42; }
  
  // file 3 contents
  export default function insideDirectory() {}
  
  // in some other file
  //不推荐
  import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
  import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
  import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export
  
  //不推荐
  import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
  import forty_two from './forty_two'; // snake_case import/filename, camelCase export
  import inside_directory from './inside_directory'; // snake_case import, camelCase export
  import index from './inside_directory/index'; // requiring the index file explicitly
  import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly
  
  //推荐
  import CheckBox from './CheckBox'; // PascalCase export/import/filename
  import fortyTwo from './fortyTwo'; // camelCase export/import/filename
  import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
  // ^ supports both insideDirectory.js and insideDirectory/index.js
  
  function makeStyleGuide() {
    // ...
  }
  export default makeStyleGuide;
  ```

- 当你导出一个构造器 / 类 / 单例 / 函数库 / 暴露的对象时应该使用帕斯卡命名法：

- ```js
  const AirbnbStyleGuide = {
    es6: {
    },
  };
  
  export default AirbnbStyleGuide;
  ```

- 缩略词和缩写都必须是全部大写或者全部小写：

- ```js
  //不推荐
  import SmsContainer from './containers/SmsContainer';
  
  //不推荐
  const HttpRequests = [
    // ...
  ];
  
  //推荐
  import SMSContainer from './containers/SMSContainer';
  
  //推荐
  const HTTPRequests = [
    // ...
  ];
  
  //推荐
  const httpRequests = [
    // ...
  ];
  
  //最佳
  import TextMessageContainer from './containers/TextMessageContainer';
  
  //最佳
  const requests = [
    // ...
  ];
  ```

- 使用可搜索的名称，名称长短应与其作用域大小相对应：

- ```js
  //若变量可能在多处使用，则应赋予便于搜索的名称
  //不推荐
  const work = 5
  
  //推荐
  const WorkDaysPerWeek = 5
  ```


### 注释

---

- 使用 `/** ... */` 作为多行注释。包含描述、指定所有参数和返回值的类型和值：

  ```js
  //不推荐
  // make() returns a new element
  // based on the passed in tag name
  //
  // @param {String} tag
  // @return {Element} element
  function make(tag) {
    // ...stuff...
    return element;
  }
  
  
  //推荐
  /**
   * make() returns a new element
   * based on the passed in tag name
   *
   * @param {String} tag
   * @return {Element} element
   */
  function make(tag) {
    // ...stuff...
    return element;
  }
  ```

- 使用 `//` 作为单行注释。在评论对象上面另起一行使用单行注释。在注释前插入空行：

  ```js
  //不推荐
  const active = true;  // is current tab
  
  //推荐
  //is current tab
  const active = true;
  
  
  //不推荐
  function getType() {
    console.log('fetching type...');
    // set the default type to 'no type'
    const type = this._type || 'no type';
  
    return type;
  }
  
  //推荐
  function getType() {
    console.log('fetching type...');
  
    //set the default type to 'no type'
    const type = this._type || 'no type';
  
    return type;
  }
  ```

- 使用 `//FIXME`: 标注问题：

  ```js
  class Calculator {
    constructor() {
        
      //FIXME: shouldn't use a global here
      total = 0;
    }
  }
  ```

- 使用 `//TODO`: 标注问题的解决方式：

  ```js
  class Calculator {
    constructor() {
        
      //TODO: total should be configurable by an options param
      this.total = 0;
    }
  }
  ```


### 工具推荐

---

##### [VS Code](https://code.visualstudio.com/)：微软出品的代码编辑器(配合以下扩展)

- React Native Tools

- React Native Snippet 

- Document This

- Guides

##### [ESLint](http://eslint.cn/)：可组装的JavaScript和JSX检查工具

##### [Flow](https://flow.org/) ：JavaScript 静态类型检查工具

##### [Watchman](https://facebook.github.io/watchman/)：监视文件系统变更的工具

##### [React Native Debugger](https://github.com/jhen0409/react-native-debugger)：功能强大的调试工具



### 参考

---

1. https://github.com/sunnylqm/react-native-coding-style
2. https://github.com/BingKui/javascript-zh#naming-conventions 
3. https://www.jianshu.com/p/3e37d488cccd 
4. [《代码整洁之道》](https://book.douban.com/subject/5442024/)

