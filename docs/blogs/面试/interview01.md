---
title: 面试1
date: 2023-08-02
tags: 
 - 面试
categories:
 - 面试
---

::: tip 
面试时长约35min
:::

## 技术相关

### 1、如何实现垂直居中

- 使用Flexbox布局：将父容器设置为flex布局，并使用align-items: center来垂直居中子元素。
```js
.parent-container {
  display: flex;
  align-items: center;
}
```
- 使用绝对定位和transform：将子元素设置为绝对定位，将top和left属性设为50%，然后使用transform属性的translate方法将元素向上移动自身高度的一半。这个方法适用于已知高度的元素。
```js
.parent-container {
  display: table;
}

.child-element {
  display: table-cell;
  vertical-align: middle;
}

```
- 使用表格布局：将父容器设置为display: table，将子元素设置为display: table-cell，并使用vertical-align: middle来垂直居中。
```js
.parent-container {
  display: table;
}

.child-element {
  display: table-cell;
  vertical-align: middle;
}

```

### 2、事件循环实现机制

**（1）created和mounted是在一个事件循环里吗，他们执行的时机有什么不同**
created 和 mounted 实际上是在同一个事件循环中执行的。

事件循环（Event Loop）是一种处理异步任务的机制，它负责管理和调度不同类型的任务。在 Vue 中，事件循环用于处理组件的生命周期钩子函数、数据更新、异步操作等。

在 Vue 的生命周期中，created 钩子函数和 mounted 钩子函数都属于同一个事件循环。它们在组件创建和挂载的过程中被触发：

created 钩子函数在组件实例被创建后立即被调用，在同一个事件循环中执行。在这个阶段，Vue 已经完成了实例的初始化，包括数据观测、计算属性等，但尚未将组件挂载到 DOM 上。

mounted 钩子函数在组件被挂载到 DOM 后调用，在同一个事件循环中执行。在这个阶段，Vue 已经将组件的模板编译成真实的 DOM，并将其插入到页面中。

需要注意的是，虽然 created 和 mounted 在同一个事件循环中执行，但它们在 Vue 生命周期中的位置不同，具有不同的作用。created 钩子在实例创建阶段执行，适合进行初始化相关的操作；mounted 钩子在 DOM 挂载阶段执行，适合进行访问 DOM 元素、操作 DOM 的操作。

**（2）request请求数据你一般是在 created还是mounted里调用**

reated 钩子函数是在组件实例创建完成后立即被调用，适合进行数据初始化和异步请求的操作。在这个阶段，组件的数据已经初始化完成，并且可以通过发送请求来获取初始数据。

而 mounted 钩子函数是在组件挂载到 DOM 后调用。在这个阶段，组件已经完全渲染，并且可以进行访问 DOM 元素和操作 DOM 的操作。通常情况下，mounted 钩子函数更适合处理与 DOM 相关的操作，例如初始化图表、绑定事件等，并不适合在这里发起数据请求。

将数据请求放在 created 钩子函数中的好处是，确保数据准备好后再进行组件的渲染，避免出现页面上存在未加载数据的空白或错误状态。同时，将数据请求放在 created 中也更符合数据初始化的逻辑和顺序。

需要注意的是，数据请求是一个异步操作，可以使用异步函数、Promise 或者其他方式来发送请求并处理返回数据。

### 3、说说weakmap和weakset，为什么用weakmap而不是map

WeakMap 是一种特殊的 Map 数据结构，其中的**键只能是对象**，而值可以是任意类型；Map 是一种常规的键值对集合，其中的**键可以是任意类型的值**。
与普通的 Map 不同，**WeakMap 对键使用弱引用**，当键**不再被其他对象引用时，垃圾回收机制会自动清除对应的键值对**。
WeakMap 没有提供像 Map 中的 size 属性来获取键值对的数量，也没有类似 Map 的 clear 方法来清空所有键值对。
你可以使用 WeakMap 的 get(key) 方法获取指定键对应的值，使用 set(key, value) 方法设置键值对，以及使用 has(key) 方法检查键是  否存在。
另外，WeakMap 实现了可迭代接口（Iterable），因此你可以使用 for...of 循环遍历 WeakMap 中的键值对。

Set 是一种集合数据结构，用于存储**唯一的值（即不允许重复）**。**Set 对象中的值可以是任意类型**，包括基本类型和对象引用。Set 通过值本身来判断是否存在重复项，并且保留了插入顺序。
**WeakSet 是一种特殊的 Set，其中的值只能是对象**。与 Set 不同的是，**WeakSet 对值使用弱引用**。当值不再被其他对象引用时，垃圾回收机制会自动从 WeakSet 中移除对应的值。
Set 允许你添加、删除和获取集合中的元素。你可以使用 add(value) 方法将值添加到 Set 中，使用 delete(value) 方法从 Set 中删除指定值，使用 has(value) 方法检查值是否存在于 Set 中。
Set 是可迭代的，你可以使用 for...of 循环遍历 Set 中的值。此外，Set 还提供了一些用于操作集合的方法，例如 size 属性用于获取集合的大小，clear() 方法用于清空集合中的所有元素。
WeakSet 没有提供像 Set 中的 size 属性或 clear() 方法来获取大小或清空集合。你只能使用 add(value) 方法将值添加到 WeakSet 中，使用 delete(value) 方法从 WeakSet 中删除指定值，使用 has(value) 方法检查值是否存在于 WeakSet 中。

::: tip 
弱引用（Weak Reference）指的是一种引用关系，在这种引用中，被引用的对象不会阻止被引用的对象被垃圾回收。
在 WeakMap 和 WeakSet 中，使用了弱引用来存储键和值（或者元素）。当一个对象作为键或值被存储在 WeakMap 或 WeakSet 中时，只要这个对象没有被其他地方引用，垃圾回收机制就有权利将其回收，并从 WeakMap 或 WeakSet 中自动移除相应的条目。
种弱引用关系使得 WeakMap 和 WeakSet 适用于存储临时数据或与对象生命周期相关的场景。当对应的键对象或元素对象不再被其他代码引用时，它们会自动从 WeakMap 或 WeakSet 中移除，无需手动进行清理操作。在使用这些数据结构时，我们通常将它们配合外部的引用来确保被引用的对象不会过早地被垃圾回收。
:::

### 12、说说symbol

### 13、说说闭包

## 比较题，日常做法题

### 3、promise.all的作用

### 4、Vue2和vue3的不同，还有两者的响应式实现的方式有什么区别

### 5、react和vue你感觉有什么不同

### 6、typescript，泛型约束

### 7、在vue和react中对对象数据进行深度操作时，你是怎么做的，是妥协地对其赋值一个新的对象吗？-我说了在useState时，考虑用proxy对对象进行代理

### 15、你们小程序是用hbuilder进行打包的吗？

### 16、你们h5也是用的uniapp打包吗？你在做h5的时候有没有遇到兼容问题样式错乱问题，是怎么解决的

## 项目相关

### next-auth内部的实现原理，他是怎么实现登录的

### 为什么选择next.js （还有你是怎么实现粘贴上传图片的