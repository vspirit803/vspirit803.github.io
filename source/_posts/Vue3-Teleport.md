---
title: Vue3 Teleport
date: 2020-08-24 11:44:24
tags:
  - Vue
  - Vue3
---

## Teleport

在项目中，某些组件可能逻辑上是一体的，但是在 UI 层面是分开的。
比如主页面有 Header 和 Main 两个部分组成，Main 部分有可能会有多个页面，每个页面都有不同的按钮要显示在 Header 的工具栏中

Vue2中一般会拆成两个组件，如 PageAMain, PageAToolbar，通过动态组件指定工具栏如何渲染。

```html
<!--App.vue-->
<template>
  <div id="Header">
    <div :is="componentName + 'Toolbar'" />
  </div>
  <div id="Main">
    <div :is="componentName + 'Main'" />
  </div>
</template>
```

而Vue3，则可以利用新增的 teleport 组件更优雅地解决这个问题
teleport 有一个必填的string类型参数to，可以是合法的选择器，该组件生效时，会把组件内部的内容渲染到to参数定位的dom节点下，如此可以将UI层面分开的部分，写在同一个组件里，例如

```html
<!--App.vue-->
<template>
  <div id="Header">
    <div id="toolbar" />
  </div>
  <Main />
</template>
```

```html
<!--Page1.vue-->
<template>
  <div class="page1">
    这是第一个页面
  </div>
  <Teleport to="#tools">
    <span>page1.工具1</span>
    <span>page1.工具2</span>
  </Teleport>
</template>
```

```html
<!--Page2.vue-->
<template>
  <div class="page2">
    这是第二个页面
  </div>
  <Teleport to="#tools">
    <span>page2.工具3</span>
    <span>page2.工具4</span>
  </Teleport>
</template>
```