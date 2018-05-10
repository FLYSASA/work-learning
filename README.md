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



