# let和const命令

## 不存在变量提升
    变量先声明后使用
```js
console.log(foo); // ReferenceError
let foo = 2;
```

## 暂时性死区（temporal dead zone，简称TDZ）
    只要块级作用域内存在let,它所声明的变量就" 绑定 "这个区域，不受外部影响
```js
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```    

    ES6明确规定，如果区块中存在let和const命令，则这个区块对这些命令声明的变量从一开始就形成了封闭的作用域，
    只要在声明前使用，就会报错
    
 ```js
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError
  
  let tmp; // TDZ结束
  console.log(tmp); // undefined
}
```   

## 不允许重复声明变量

```js
//报错
function f() {
  let a = 10;
  var a = 1;
}

function f1(arg) {
  let arg; // 报错
}
```

## const 定义的变量的值不能改变，但是对象可以
    彻底冻结对象Object.freeze()

```js
const constantize = (obj) => {
  Object.freeze(obj);
  Object.keys(obj).forEach((key, value) => {
    if (typeof obj[key] === 'object') {
      constantize(obj[key]);
    }
  })
}
```    
 
## const 设置的变量只在当前模块有效
```js
// const.js
export const A = 1;
// test1.js
import { A } from './const';
// test2.js
import * as consts from './const';
console.log(consts.A);
```   



