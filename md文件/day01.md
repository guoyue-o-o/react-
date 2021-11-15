# 1.react优点
- 1.原生js操作dom复杂，效率低（DOM-API操作ui）
- 2.使用js直接操作dom,引起大量重绘重排
- 3.原生js不能组件化，代码复用率低

## 模块化：
- 理解：向外提供特定功能的js程序（js文件）
- 把大文件拆分成小文件（主要用来拆分js）
## 组件化：
- 理解  ：用来实现局部功能效果的代码和资源的集合(html/css/js/images)
- 一个界面得到功能更复杂
- 复用编码，简化项目编码，提高运行效率

# 2. react特点：
- 1.采用组件化模式，声明式编码，提高开发效率以及组件复用率
- 2.rn中可以用react进行移动端开发
- 3.使用虚拟dom技术+优秀的diffing算法，尽量减少与真实dom的交互

# 3. babel:
将jsx===》js;

# 4. 虚拟dom
## 特点
- 本质是Object类型的对象（一般对象）
- 虚拟dom比较轻便（属性少），真实dom比较重（属性多），因为虚拟dom是react内部在使用，不需要真实dom上那么多属性
- 虚拟dom最终会被react转换成真实dom，呈现在页面上

# 5. jsx
- 简化创建元素
- 返回一个对象
- 不是字符串也不是html标签

# 6. jsx语法规则
- 1.定义虚拟dom时不要写引号
- 2.标签中混入js表达式要用{}
- 3.样式的类名要用className
- 4.内联样式，要用style={{}}
- 5.只有一个跟标签
- 6.标签必须闭合
- 7.标签首字母
  - 若字母是小写字母，则将标签转为html中同名元素，若没有，则报错
  - 若大写开头，react无渲染对应组件，组件没有，报错

# 7.
## js语句（代码）
一般控制代码走向
- if(){}
- for() 
- switch case

## js表达式
- 一个表达式会产生一个值，可以放在任何一个需要值的地方
- 例如：
  - ① a
  - ② a + 
  - ③ arr.map()
  - ④ demo(1)
  - ⑤ function test() {}

# 8. 面向组件编程

# 9. 类
- 1.类中的构造器不是必须写的，要对实例进行一些初始化的操作，如添加指定属性时才写
- 2.如果A类中继承了B类，且A类中写了构造器，那么A类构造器中的super是必须要调用的
- 类中所有定义的方法，都放在了类的原型对象上，供实例去使用


## 函数式组件
**适用于简单组件**

使用：
- 解析标签，找到组件
- 发现组件是用函数定义的，调用该函数，将返回的虚拟dom转成真实dom


## 类式组件

**适用于复杂组件**
- 必须继承extends React.Component
- 必须有render
- render必须有返回值

render也是放在类的实例对象上的，render中的this指向组件实例对象

使用：
- 解析组件标签，找到组件
- 发现组件是类定义的，随后new出类的实例，并通过实例调用到原型上的render方法
- 将render返回的虚拟dom转换成真实dom


**类中定义的方法，默认在局部开启了严格模式**

**严格模式可以在局部开**


```
class Person() {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    speak() {
        console.log(this.name)
    }
}

// p1 是类的实例，speak定义在了类的原型对象上，供类的实例使用
const p1 = new Person('tom', 18);
// 实例调用
p1.study() // tom


// 赋值语句, 将study方法赋值给p2
const p2 = p1.study;
// 类中定义的方法默认开始严格模式，严格模式下的this指向undefined（非严格模式指向window）
// 直接调用
p2(); // undefined

```

构造器
- 初始化状态
- 改变this指向问题（bind）  


### 复杂组件——有状态
### 简单组件——无状态

组件的状态里边存着数据，数据驱动页面的改变，组件实例上存在这state对象，可以定义组建的初始状态


对标签属性进行类型必要性的限制
PropTypes
```

方法一：
class Person extends React.Component {
    state = {

    }
    render() {

    }
}
Person.propTypes = {
    name: PropTypes.string.isRequired, // 字符串类型，必填
    age: PropTypes.number,
    speak: PropTypes.func,
}

// 默认值
Person.defaultProps = {
    age: 18
}


方法二：
class Person extends React.Component {
    static propTypes = {
         name: PropTypes.string.isRequired, // 字符串类型，必填
         age: PropTypes.number,
         speak: PropTypes.func,
    }
     static defaultProps = {
       age: 18
    }
    state = {

    }
    render() {

    }
}

```

# 10. refs

**请勿过度使用ref**

发生事件的元素跟要操作的元素是同一个元素，可以省略ref

- 用于获取dom元素
- 条件允许的情况下，尽量减少使用字符串形式的ref

## 分类
### 1. 字符串形式的ref（**不建议使用，因为有效率问题**）
```
// 定义
<input ref='input1' />

// 使用
this.refs.input1
```
### 2. 回调形式
```
// 将当前节点挂载在实例对象身上
<input ref={(c) => this.input2 = c} />

// 使用
 this.input2
```

回调ref中回调执行次数
  更新阶段执行两次，先赋值为Null，然后再赋值

### 3. createRef（**React最推荐**）

```

// React.createRef调用后可以返回一个容器，该容器可以储存ref标识的节点
// 该容器是专人专用的，有几个ref就要创造几个ref的容器
myRef = React.createRef()

myRef2 = React.createRef()

// 把input放到myRef容器中
<input ref={this.myRef} />

<input ref={this.myRef2} />

```

# 11. React事件处理

1.通过onXxxx属性指定时间处理函数(**大小写**)
- React使用的是自定义（合成）事件，不是使用的原生的dom事件————为了更好的兼容性
- React使用的是事件委托方式处理（委托给最外层元素）————为了高效
```
<!-- 事件委托---事件冒泡 -->
<!-- li的事件可以定义给ul -->
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>

```
# 12. 



