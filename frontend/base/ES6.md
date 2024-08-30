<img src="../../images/es6/es6.jpeg" style="zoom: 60%">

ES 全称 EcmaScript，是脚本语言的规范，而平时经常编写的 JavaScript，是 EcmaScript 的一种实现，所以 ES 新特性其实指的就是 JavaScript 的新特性。

ES6 可以去看看[阮一峰的 ES6 教学](https://es6.ruanyifeng.com/#README)

### 一、ECMASript 相关介绍

1. <strong style="color: red">JavaScript 基本语法</strong>
2. AJAX 和 NodeJS

### 二、ECMASript6 新特性（基础）

#### 2.1 let 关键字

let 关键字用来声明变量，使用 let 声明的变量有几个特点：

1. 不允许重复声明

```js
let star = '周董';
let star = 'JJ'; // Uncaught SyntaxError: Identifier 'star' has already been declared (at learnES6.html:22:9)
```

2. 块级作用域（全局 函数 eval）

```js
{
  let car = '五菱';
}
console.log(car); // Uncaught ReferenceError: car is not defined at learnES6.html:28:17
```

3. 不存在变量提升

```js
console.log(song); // undefined 变量提升
var song = '恋爱达人';

console.log(song); // Uncaught ReferenceError: Cannot access 'song' before initialization at learnES6.html:32:17
let song = '恋爱达人';
```

4. 不影响作用域链

```js
{
  let school = '尚硅谷';
  function fn() {
    console.log(school);
  }

  fn(); // 尚硅谷
}
```

<strong style="color: blue">应用场景：以后声明变量使用 let 就对了</strong>

#### 2.2 const 关键字

const 关键字用来声明常量，const 声明有以下特点

1. 声明必须赋初始值

```js
  const A; // Uncaught SyntaxError: Missing initializer in const declaration (at learnES6.html:51:11)
```

2. 标识符一般为大写（潜规则）
3. 不允许重复声明
4. 值不允许修改
5. 块级作用域

<strong style="color: red"> ⚠️ 注意：对象属性修改和数组元素变化不会出发 const 错误（其实是常量指向的地址没有修改）</strong>

```js
const TEAM = ['UZI', 'MLXG', 'Letme'];
TEAM.push('MeiKou');
```

<strong style="color:blue">应用场景：声明对象类型使用 const，非对象类型声明选择 let</strong>

#### 2.3 变量的解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构赋值。

1. 数组的结构

```js
const F4 = ['小沈阳', '刘能', '赵四', '宋小宝'];

let [xiao, liu, zhao, song] = F4;

console.log(xiao); // 小沈阳
console.log(liu); // 刘能
console.log(zhao); // 赵四
console.log(song); // 宋小宝
```

2. 对象的结构

```js
let zhao = {
  name: '赵本山',
  age: '不详',
  xiaopin: function () {
    console.log('我可以演小品');
  },
};

// 赋值的名字和对象内的必须相同
let { name, age, xiaopin } = zhao;

console.log(name); // 赵本山
console.log(age); // 不详
console.log(xiaopin);
/*
    f() {
      console.log('我可以演小品');
    }
  */
```

<strong style="color: red">⚠️ 注意：频繁使用对象方法、数组元素，就可以使用解构赋值形式</strong>

#### 2.4 模板字符串

模板字符串（template string）是增强版的字符串，用反引号（`）标识，特点：

1. 字符串中可以出现换行符
2. 可以使用 ${xxx} 形式输出变量

```js
let star = '王宁';
// 变量拼接
let result = `${star}在前几年离开了开心麻花`;
console.log(result); // 王宁在前几年离开了开心麻花
```

<strong style="color: red">⚠️ 注意：当遇到字符串与变量拼接的情况使用模板字符串</strong>

#### 2.5 简化对象写法

ES6 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```js
let name = '西岸';
let say = function () {
  console.log('我会说英语');
};

const student = {
  name,
  say,
  hobby() {
    console.log('我喜欢打羽毛球');
  },
};

console.log(student); // {name: '西岸', say: ƒ}
```

#### 2.6 箭头函数

ES6 允许使用「箭头」（=>）定义函数

```js
// 1. 通用写法
let fn = (arg1, arg2, arg3) => {
  return arg1 + arg2 + arg3;
};
```

箭头函数的注意点:

1. 如果形参只有一个，则小括号可以省略

```js
  let fn2 = num => {
    console.log(num));
  }
```

2. 函数体如果只有一条语句，则花括号可以省略，函数的返回值为该条语句的执行结果

```js
const fn3 = (data) => data;
```

3. 箭头函数 this 指向声明时所在作用域下 this 的值

```js
function getName() {
  console.log(this.name);
}

let getName2 = () => {
  console.log(this.name);
};

// 设置 window 对象的 name
window.name = '尚硅谷';

const school = {
  name: 'ATGUIGU',
};

// 直接调用
getName(); // 尚硅谷
getName2(); // 尚硅谷

// call调用
getName.call(school); // ATGUIGU
getName2.call(school); // 尚硅谷
```

4. 箭头函数不能作为构造函数实例化

```js
let Person = (name, age) => {
  this.name = name;
  this.age = age;
};

let me = new Person('xiao', 30);

console.log(me); // Uncaught TypeError: Person is not a constructor at learnES6.html:161:14
```

5. 不能使用 arguments 参数

```js
let fn = () => {
  console.log(arguments);
};

fn(); // Uncaught ReferenceError: arguments is not defined at fn (learnES6.html:168:19) at learnES6.html:171:5
```

<strong style="color: red">⚠️ 注意：箭头函数不会更改 this 指向，适合与 this 无关的回调，用来指定数组、定时器的回调函数会非常合适</strong>

#### 2.7 rest 参数

ES6 引入 rest 参数，用于获取函数的实参，用来代替 arguments，rest 参数非常适合不定个数参数函数的场景

```js
function date() {
  console.log(arguments);
}

date('bai', 'red', 'blue');

// rest 参数
function date2(...args) {
  console.log(args);
}

date2('中国', '美国', '俄罗斯');
```

#### 2.8 spread 扩展运算符

扩展运算符（spread）也是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列，对数组进行解包。

```js
let tfboys = ['德玛西亚之力', '德玛西亚之翼', '德玛西亚皇子'];

function fn() {
  console.log(arguments);
}

fn(tfboys); // fn(['德玛西亚之力', '德玛西亚之翼', '德玛西亚皇子'])

fn(...tfboys); // fn('德玛西亚之力','德玛西亚之翼','德玛西亚皇子')

// 应用
const kz = ['小杨', '大杨'];
const fh = ['玲花', '曾毅'];

// 拼接 ES5
const kzfh = kz.concat(fh);
console.log(kzfh); // ['小杨', '大杨', '玲花', '曾毅']

// ES6
const kzfh2 = [...kz, ...fh];
console.log(kzfh2); // ['小杨', '大杨', '玲花', '曾毅']
```

#### 2.9 Symbol（用的比较少，可以跳过）

**Symbol 基本使用**
ES6 引入了一种新的原始数据类型 Symbol, 表示独一无二的值。它是 JavaScript 语言的第七种数据类型，是一种类似于字符串的数据类型。

> 七种类型
> USONB you're so niubility
> u - undefined
> s - string sy,bol
> o - object
> n - null number
> b - boolean

**Symbol 特点**

1. Symbol 的值是唯一的，用来解决命名冲突的问题

```js
// 创建symbol
let s = Symbol();
console.log(s, typeof s); // Symbol() 'symbol'
// 或
let s2 = Symbol('尚硅谷');
let s3 = Symbol('尚硅谷');

console.log(s2 === s3); // false

// Symbol.for 创建
let s4 = Symbol.for('尚硅谷');
console.log(s4, typeof s4); // Symbol(尚硅谷) 'symbol'
```

2. Symbol 值不能与其他数据进行运算
3. Symbol 定义的对象属性不能使用 `for…in` 循环遍历，但是可以使用 `Reflect.ownKeys` 来获取对象的所有键名

<strong style="color: red">⚠️ 注意: 遇到唯一性的场景时要想到 Symbol</strong>

### 三、 🌟Promise

#### 3.1 Promise 介绍与基本使用

<strong style="color: red">Promise</strong> 是 JS 中进行异步编程的**新解决方案**（备注：旧的解决方案是-> 单纯的使用回调函数）

从语法上来说：Promise 是一个构造函数
从功能上来说：Promise 对象用来封住一个异步操作并可以获取其成功/失败的结果

==Promise 支持链式调用，可以解决回调地狱问题==

> Promise 基本使用

<img src="../../images/es6/promise_exp1.png" style="zoom: 50%">

> Promise 🌟 状态

Promise 实例对象中有一个属性`「PromiseState」` 一共有三种状态

1. pending 未决定的
2. resolved / fullfilled 成功
3. reject 失败

⚠️：状态改变只有`pending -> resolved`和`pending -> reject`着两种，且一个 promise 对象==只能改变一次==。无论变为成功还是失败，都会有一个结果数据（value / reason）。

> Promise 对象的值

Promise 实例对象中的另一个属性 `「PromiseResult」`，保存着对象成功/失败的结果，只有 resolve/reject 可以改变值

> Promise 流程

<img src="../../images/es6/promise流程.png" style="zoom: 70%">

#### 3.2 Promise API

1. **resolve** （传入非 promise 对象，则返回一个成功的 promise 对象；传入的是一个 promise 对象，则返回这个传入 promise 对象的结果）
2. **reject**（无论传入什么，返回的都是失败的 promise 对象）
3. **all**（参数包含 n 个 promise 的数组，返回一个新的 promise，只有所有的 promise 都成功才成功，只要有一个失败了就直接失败）
4. **race**（参数包含 n 个 promise 的数组，返回一个新的 promise，第一个完成的 promise 的结果状态就是最终的结果状态）
   ...

#### 3.3 Promise 自定义封装

...

#### 3.4 async 与 await

- **asnyc**（如果返回值是一个非 Promise 类型的数据，则返回一个成功的 Promise 对象；如果返回的是一个 Promise 对象，则返回这个传入 promise 对象的结果）
  <img src="../../images/es6/async.png" style="zoom: 70%">

- **await**
  - 1.右侧的表达式一般为 promise 对象，但也可以是其它的值；
  - 2.如果表达式是 promise 对象，await 返回的是 promise 成功的值；
  - 3.如果表达式是其它值，直接将此值作为 await 的返回值；

注意 ⚠️：

1. await 必须写在 async 函数中，但 async 函数中可以没有 await
2. 如果 await 的 promise 失败了，就会抛出异常，需要通过 try...catch 捕获处理
