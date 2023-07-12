---
title: "📚︎ Vue3中 Watch和watchEffect的区别"
date: 2022-09-03 21:38:11
updated: 2023-07-10 21:06:06
tags: [Css, JavaScript, 前端]
categories: 前端样式
keywords:
description:
top_img: https://images.unsplash.com/photo-1688725755373-10d1bb23b55d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1770&q=80
comments:
cover: https://images.unsplash.com/photo-1688725755373-10d1bb23b55d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1770&q=80
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
### 一、监听基础类型

```jsx
const nums = ref(9)

watch(nums, (newValue, oldValue) => {
	console.log('watch 已触发', newValue)
})
```
### 二、监听复杂类型
```jsx
const demo = reactive({
  name: '前端小玖',
  nickName: '小玖',
  soulmate: {
    name: '',
    nickName: ''
  }
})
```
复杂类型的监听有很多种情况，具体的内容如下
#### 1.监听整个对象
```jsx
watch(demo, (newValue, oldValue) => {
	console.log('watch 已触发', newValue)
})
```

其第一个参数是直接传入要监听的对象。当监听整个对象时，只要这个对象有任何修改，那么就会触发 watch 方法。无论是其子属性变更（如 demo.name），还是孙属性变更（如 demo.soulmate.name）...，都是会触发 watch 方法的。

#### 2.监听对象中的某个属性
```javascript
// 监听demo对象的name属性
watch(() => demo.name, (newValue, oldValue) => {
	console.log('watch 已触发', newValue)
})
```

如上代码，监听 demo 对象的 name 属性，那么只有当 demo 对象的 name 属性发生变更时，才会触发 watch 方法，其他属性变更不会触发 watch 方法。注意，此时的第一个参数是一个箭头函数。
#### 3.只监听对象的子属性
```javascript
watch(() => ({ ...demo }), (newValue, oldValue) => {
	console.log('watch 已触发', newValue)
})
```

这种情况，只有当 demo 的子属性发生变更时才会触发 watch 方法。孙属性，曾孙属性... 发生变更都不会触发 watch 方法。也就是说，当你修改 demo.soulmate.name 或者 demo.soulmate.nickName 时是不会触发 watch 方法的。
#### 4.监听对象的所有属性
```javascript
watch(() => demo, (newValue, oldValue) => {
	console.log('watch 已触发', newValue)
}, { deep: true })
```

这个相当于监听整个对象（效果与上面的第一种相同）。但是实现方式与上面第一种是不一样的，这里我们可以看到，第一个参数是箭头函数，并且还多了第三个参数 { deep: true }。当加上了第三个参数 { deep: true }，那么就不仅仅是监听对象的子属性了，它还会监听 孙属性，曾孙属性 ...

通常要实现监听对象的所有属性，我们都会采用上面第一种方法，原因无他，第一种编码简单，第一个参数直接传入 demo 即可。
### 三、组合监听
```javascript
const nums = ref(9)
const demo = reactive({
  name: '前端小玖',
  nickName: '小玖',
  soulmate: {
      name: '',
      nickName: ''
    }
})
```

什么是组合监听呢？举个例子，比如我想同时监听 demo 对象的 name 属性，和基础类型 nums，只要他们其中任何一个发生变更，那么就触发 watch 方法。
```javascript
watch([() => demo.name, nums], ([newName, newNums], [oldName, oldNums]) => {
  console.log('watch 已触发: name', newName)
  console.log('watch 已触发: nums', newNums)
})
```

注意，此时的第一个参数是一个数组，且第二参数箭头函数的参数也是数组的形式。
#### 四、其他

与 VUE2 中的 watch 不同，VUE3 可以多次使用 watch 方法，通过多个watch 方法来监听多个对象。而 VUE2 则是把所有的要监控的对象放在 watch 里面。

VUE2 代码：
```javascript
watch: {
  nums () {},
  'demo.name' () {}
}
```

VUE3 代码：

```javascript
watch(nums, () => {})
watch(() => demo.name, () => {})
```

关于 watch 的第三个参数，除了布尔类型的 deep，还有一个布尔类型的 immediate。源码中的接口声明如下：

```javascript
export declare interface WatchOptions<Immediate = boolean> extends WatchOptionsBase
{
  immediate?: Immediate;
  deep?: boolean;
}
```
