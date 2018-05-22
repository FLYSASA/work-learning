# ECMAScript 6

### 1. var、let、const变量声明区别

- var : 使用var声明的变量,其作用域为该语句所在的函数内,且存在变量提升现象

- let : 使用let声明的变量,其作用域为该语句所在的代码块内,不存在变量提升

- const: 使用const声明的是常量,在后面出现的代码中不能再修改该常量的值.


### 2. 变量的解构赋值
ES6 允许按照一定模式,从数组和对象中提取值,对变量进行赋值,这被称为解构.

如以前为变量赋值,只能直接指定值.
```js
let a = 1
let b = 2
let c = 3
```

ES6 允许写成这样:
```js
let [a,b,c] = [1,2,3]
```
从数组中提取值,按照对应位置,对变量赋值.

本质上,这种写法属于"模式匹配",**只要等号两边的模式相同,左边的变量就会被赋予对应的值.**

如果解构不成功,变量的值就等于`undefined`.

如:
```js
let [foo] = []
let [bar,foo] = [1]
```

**对象解构赋值:**
```js
let {foo,bar} = {foo:"aaa",bar:"bbb"}
```
对象的解构与数组有一个重要的不同.**数组的元素是按次序排列的,变量的取值由它的位置决定,而对象的属性没有次序,变量必须与属性同名**


###3 模板字符串的写法
模板字符串使用反引号 (\` \`) 来代替普通字符串中的用双引号和单引号。模板字符串可以包含特定语法（${expression}）的占位符。

以前:
```js
var a = 5
var b = 10
console.log('Fifteen is ' + (a + b) + ' and\nnot ' + (2 * a + b) + '.')
```

使用模板字符串:
```js
var a = 5;
var b = 10;
console.log(`Fifteen is ${ a + b } and\nnot ${2*a + b}`)
```

注意模板字符串使用的是反引号.


###4 ES6默认参数值
es6中函数可以设置参数默认值:
```js
function test(x,y=1){
    console.log(x,y)
}
test(10) //10 1  y使用了默认值
```

###5 ES6箭头函数
箭头函数用 `=>` 符号来定义
其相当于匿名函数,所以采用函数表达式的写法
左边是传入函数的参数,右边是函数中执行的语句.
```js
var sum = (x,y) => {return x + y;}
//相当于
var sum = function(x,y){
    return x + y;
}
```

完整的写法,左边小括号,右边大括号,而下面的情况可以简写:

1. 当要执行的代码块只有一条return语句时,可省略大括号和return关键字
```js
var sum = (x,y) => x + y;
```
2. 当传入的参数只有一个时,可以省略小括号
```js
var square = x => x * x
```
3. 当不需要参数时,使用空的圆括号
```js
var one = () => 1
```

箭头函数在回调函数中非常简洁,像这样:
```js
var array = [1,2,3]
var result = array.map(x => x*x); // [1,4,9] 遍历数组运算
```

**需要注意的是箭头函数没有自己的`this,arguments,super,new.target`,它们分别指向外层函数的相应变量**

###6 promise对象
1. then()方法
2. 链式调用
3. 创建一个Promise


###7 export命令,export default命令,import命令

##### export:
用于在创建JavaScript模块时,从模块中导出函数,对象或原始值,以便其他程序可以通过import语句使用它们.

##### export和export default的区别:
1. export 与 export default均可用于导出常量、函数、文件、模块等
2. 你可以在其它文件或模块中通过`import+(常量 | 函数 | 文件 | 模块)`名的方式,将其导入,以便能够对其进行使用
3. 在一个文件或模块中,**export和import可以有多个,export default仅有一个**
4. 通过export方式导出,在导入时要加`{}`,export default则不需要

##### 使用export default命令,为模块指定默认输出,这样就不需要知道所要加载模块的变量名. (在引入模块的文件中可以自定义引入的模块的名字)

参考: https://blog.csdn.net/zhou_xiao_cheng/article/details/52759632


# webpack2 文档
- **webpack模块概念**
它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源.还可以将按需加载的模块进行代码分隔,等到实际需要的时候再异步加载. 通过loader的转换,任何形式的资源都可以视作模块,比如CommonJs模块,AMD模块,ES6模块,CSS,图片,JSON,Coffeescript,less等. 

- **四个核心概念**
1. 入口(Entry)
应用程序的入口起点认为是 **根上下文或app第一个启动文件**
在webpack中,我们使用webpack配置对象中的`entry`属性来定义入口
```js
module.exports = {
    entry: './path/to/my/entry/file.js'
}
```

2.出口(output)
将所有的资源(assets)归拢在一起后,我们还需要告诉webpack在哪里打包我们的应用程序,webpack的`output`属性描述了如何处理归拢在一起的代码.
...


# vue-router 

### 首先明确三个基本概念: route,routes,router

1. route 
这是一条路由,它是单数,Home按钮 => home内容,这是一条route. 它将点击按钮与页面联系起来

2. routes
这是一组路由,把上面的每一条路由组合起来,形成一个数组. `[{Home按钮 => home内容},{about按钮 => about内容}]`,routes即由多条route组成的数组

3. router
router是一个机制,相当于一个管理者,它来管理路由. 因为routes只是定义了一组路由,它放在那里是静止的,当真正来了请求,怎么办? 就是当用户点击home按钮的时候,怎么办? 这时router就起作用了,它到routes中去查找,去找到对应的home内容,所以页面中就显示了home内容.

客户端中的路由,实际上就是dom元素的显示和隐藏. 当页面中显示home内容的时候,about中的内容全部隐藏.客户端路由有两种实现方式: 基于hash和基于html5 history api.

**vue-router中的路由也是基于上面的内容来实现的**

在vue中我们的页面中所有内容都是组件化的,我们只要把路径和组件对应起来就可以了,然后在页面中把组件渲染出来.

具体实现步骤:
1. 在html模板中
```js
//app.vue
<header>
    <router-link to="/home">Home</router-link>   
    <router-link to="/about">About</router-link>
</header>

<router-view/>
```
定义`router-link`和`router-view`两个标签,来对应点击和显示部分.  `router-link`就是定义页面点击的部分,`router-view`定义显示部分,就是点击后页面出现在什么地方.

2. js中配置路由
既然使用了router标签,所以需要定义router即配置路由,在src文件夹下新建`router.js`,**定义路径到组件的映射**
```js
import Vue from 'vue'
import VueRouter from 'vue-router'

//引入组件,在app.vue中就不需要再引入了,只需要两个router标签即可
import home from './components/home.vue'
import about from './components/about.vue'

//告诉vue使用 VueRouter
Vue.use(VueRouter)

const routes = [   //定义映射关系
    {
        path: "/home",
        component: home
    },
    {
        path: '/about',
        component: about
    }
]

var router = new VueRouter({
    routes         //将routes作为对象参数传给VueRouter的实例
})

export default router; //导出router
```

3. 把路由注入到根实例中,启动路由.
```js
//main.js
import router from "/router.js"   //引入组件
new Vue({
    router
})
```