---
title: "🍖头疼的面试题"
date: 2024-10-21 15:38:11
updated: 
tags: [Css, JavaScript]
categories: 面试
keywords:
description:
top_img: https://images.pexels.com/photos/10486875/pexels-photo-10486875.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1
comments:
cover: https://images.pexels.com/photos/10486875/pexels-photo-10486875.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1
toc:
toc_number:
toc_style_simple:
copyright: false
copyright_author:
copyright_author_href: false
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:

---

### 🔔面试啦


>
> * 掌阅科技一面 
> * 1h 全是技术
> * 头疼
> * 2024-10-21 
> 

#### 1: 函数作用域
```javascript
let name = 'foo';

function F() {
    console.log(name)
}

(() => {
    let name = 'test'
    F()
})()
```
> let name = 'foo'; 在全局作用域中声明了一个变量 name。函数 F() 打印了变量 name。由于 F() 是在全局作用域中定义的，所以当它被调用时，会从全局作用域查找 name。在立即执行函数表达式（IIFE）中，使用 let 声明了一个新的变量 name。这个 name = 'test' 仅存在于 IIFE 的作用域中，不会影响全局的 name。当在 IIFE 中调用 F() 时，它会查找定义 F() 时所在的作用域中的 name（即全局作用域），而全局作用域中的 name 仍然是 'foo'。因此，F() 中的 console.log(name) 打印的是 'foo'。

#### 2：原型链

```javascript

Function.prototype.a = 'a'
Object.prototype.b = 'b'

const F = new Function;

console.log(F.a)
console.log(F.b)
```
> Function.prototype.a = 'a'; 为所有函数的原型添加了属性 a。这意味着任何函数（因为它们继承自 Function.prototype）都可以访问这个属性。
> Object.prototype.b = 'b'; 为所有对象的原型添加了属性 b。因为 JavaScript 中所有对象最终都继承自 Object.prototype，这个属性对所有对象都是可访问的，包括函数（因为函数也是对象）。
> const F = new Function; 创建了一个新的函数对象。F 现在是 Function 的一个实例，而函数也继承自 Object。
>因此，当你打印以下内容时： console.log(F.a); 会输出 'a'，因为 F 是一个函数，继承自 Function.prototype，而 Function.prototype 上有属性 a。 console.log(F.b); 会输出 'b'，因为 F 是一个函数，函数也继承自 Object.prototype，而 Object.prototype 上有属性 b。
#### 3: Promise


```javascript
try {
  Promise.resolve(Promise.reject(new Error('这是错误')))
  console.log('111')
} catch {
  console.log('222')
}

```


#### 4: 函数柯里化和闭包

```javascript
// 实现一个函数

const subNum = (...arg) => arg.reduce((acc, curr) => acc + curr, 0 );

const someFunction = () {
  //wirte your code
}

const add = someFunction(subNum);

const sum = add(1,2)(3)(4)()

console.log(sum) // 10

```

```javascript
const someFunction = () {
  //wirte your code
  
}

```

#### 5: Symbol.instance了解过吗



#### 6: scss中函数作用

`@include` 

`@extends`

#### 7: [...'static']结果



