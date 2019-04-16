# vue_demo1.1学习笔记

## RUN

```
Vue Create vue_demo1.1
```

```
npm run serve
```

[TOC]



## 知识储备

------

##### :class`**绑定**

我们可以向 `v-bind:class` 传入一个对象，来动态地切换 class：

对象语法`<div v-bind:class="{ active: isActive }"></div>`

上述语法意味着，`active` 这个 class 的存在与否，取决于 `isActive` 这个 data 属性的 [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) 值。

------

##### **数组语法**

我们可以向 `v-bind:class` 传入一个数组，来与 class 列表对应：

```
<div v-bind:class="[activeClass, errorClass]"></div>
```

如果有多个条件 class 时，就会显得有些繁琐。这也就是为什么还可以在数组语法中使用对象语法

------

##### **按键修饰符**

在监听键盘事件时，我们经常需要检查详细的按键。Vue 允许为 `v-on` 在监听键盘事件时添加按键修饰符：

例如 `v-on:keyup.enter` .enter/.tab/.delete/.esc/.space/.up/.dowm/.left/.right

你可以直接将 [`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values) 暴露的任意有效按键名转换为 kebab-case 来作为修饰符。

```
<input v-on:keyup.page-down="onPageDown">
```

在上述示例中，处理函数只会在 `$event.key` 等于 `PageDown` 时被调用。

------

##### **事件名称**（event names）

你可以直接将 [`KeyboardEvent.key`](https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent/key/Key_Values) 暴露的任意有效按键名转换为 kebab-case 来作为修饰符。

```
<input v-on:keyup.page-down="onPageDown">
```

在上述示例中，处理函数只会在 `$event.key` 等于 `PageDown` 时被调用。

与 components 和 props 不同，事件名称永远不会用作 JavaScript 变量或属性名称，所以没有理由去使用驼峰式命名(camelCase)或帕斯卡命名(PascalCase)。此外，DOM 模板中的 `v-on` 事件监听器会自动转换为小写（这是因为 HTML 属性名称不区分大小写），所以 `v-on:myEvent` 会变为 `v-on:myevent` - 由此 `myEvent` 就不可能监听到事件触发。

由于这些原因，我们建议你**总是使用串联式命名(kebab-cased)来命名事件名称**。

------

##### **V-model**

在一个组件中，`v-model` 默认使用 `value` 作为 prop，以及默认使用 `input` 作为监听事件，然而，对于某些类型的 input 元素（例如 checkbox 和 radio），由于这些类型的 input 元素本身具有 [不同用法](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox#Value)，可能会占用 `value` 特性。在这种情况下，使用组件的 `model` 选项可以避免冲突

```
Vue.component('base-checkbox', {
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    checked: Boolean
  },
  template: `
    <input
      type="checkbox"
      v-bind:checked="checked"
      v-on:change="$emit('change', $event.target.checked)"
    >
  `
})
```

------

##### Prop**类型**

通常，你会希望每个 prop 都对应指定类型的值。在这些场景中，你可以将 props 展示为对象，其中每个属性的名称和值，分别包含 prop 名称和类型：

```
props: {
  title: String,
  likes: Number,
  Click: Function,
  isPublished: Boolean,
  commentIds: Array,
  author: Object
}
```

## NO.1配置文件

------

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/0.png?raw=true)

引入base.css	/	index.css	/	index.html	/并在App.vue中引入

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/2.png?raw=true)

成功引入后会显示

![](https://github.com/zhuayu/combat-todo/raw/master/todo.png)

接下来任务开始我们先把数据渲染上去使用到 

1. 在 Vue.data 中定义 todos，todo 包含 title、completed
2. 在 templete 中使用 for 绑定 todos 数据进行渲染



###### ![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/4.png?raw=true)

<u>对于这里关于:key我有查找了一些知识进行补充</u>

<u>key是给每一个vnode的唯一id,可以`依靠key`,更`准确`, 更`快`的拿到oldVnode中对应的vnode节点。</u>

<u>key的作用就是更新组件时**判断两个节点是否相同**。相同就复用，不相同就删除旧的创建新的。</u>

<u>带上唯一key虽然会增加开销，但是对于用户来说基本感受不到差距，而且能保证组件状态正确，这应该就是为什么推荐使用唯一id作为key的原因。</u>

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/5.png?raw=true)

完成后我们成功把数据渲染到了Todolist中

## 列表修改

任务要求：

1. 双击 todo 内容，其下面的 input 聚焦
2. 对 todo 的 input 修改后失去焦点或者按回车键，返回原来 todo 状态并展示修改后的内容

任务提示：

1. 为 todo 中 label 元素绑定 dbclick 事件，当点击 todo 时候把 todo 存储到 Vue.data.editTodo 属性中，同时把当前的 title 存储到 Vue.data.beforeEditCache 作为缓存，方便撤销操作。
2. 在 todos 渲染中判断，如果 editTodo 等于该 todo 则显示编辑状态并且其 input 聚焦
3. 为 input 元素于 todo.title 进行双向绑定，当修改 input 时同时修改 title 属性
4. 为 input 绑定键盘事件与失去焦点事件，当时机出发时设置 editTodo 为 Null 返回原来状态。
5. 为 input 绑定 ese 取消事件，取 beforeEditCache 的值重设。

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/6.png?raw=true)

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/7.png?raw=true)

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/6-1.png?raw=true)

## 状态切换

任务要求：

1. 点击完成的 todo 左侧状态按钮，切换为未完成
2. 点击未完成的 todo 左侧状态按钮，切换未完成
3. 单击顶部全选按钮，如果未全选切换所有 todo 为全选
4. 点击顶部全选按钮，如果全选切换所有 todo 为未全选

任务提示：

1. 为 checkbox 双向绑定 todo.completed 属性
2. 为 Vue.computed 添加 allDone ，其 get 读取属性返回当前所有 todos 的 completed 是否为 true，其 set 设置所有 todos 的 completed 值为当前 get 值的反选择。

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/8.png?raw=true)

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/8-1.png?raw=true)

## 添加项目

本任务中，我们为列表添加多一项，当用户在顶部输入框输入时，当按钮下回车键时候，为列表中添加当前项目，title 为输入值，状态为未完成。

任务要求：

1. 在输入框中输入完毕，按回车键，往列表中添加未完成的一项

任务提示：

1. 为顶部输入框绑定监听回车事件，事件触发时候为 todos 数据中 push 一项，同时讲当前 value 设置为空。

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/9.png?raw=true)

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/9-1.png?raw=true)

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/9-2.png?raw=true)

## 删除项目

本任务中，我们需要来完成删除项目的功能。删除场景主要有 2 个，一个为在 todo hover 之后的右侧有一个关闭按钮，当点击关闭按钮时候删除当前 todo 项目。在脚步导航的右侧有一个删除所有已完成的按钮，点击删除所有已完成的 todo 项目。

任务要求：

1. 完成单条 todo 删除功能
2. 完成所有已完成的 todo 删除功能

任务提示：

1. 为删除按钮绑定点击事件，点击在 todos 移除当前自己的项目
2. 为删除所有按钮绑定点击事件，点击 todos.filter 一下 todo 重新设置 todos

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/10.png?raw=true)

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/10-1.png?raw=true)

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/10-2.png?raw=true)

## 项目筛选

在底部导航位置有三个状态，分别为 all、active、completed，全部、进行中、已完成的意思，在本次任务中，我们需要筛选切换不同的状态来动态展示对应状态的数据。

任务要求：

1. 默认在 all 状态，展示所有状态 todo 。
2. 点击 active 状态，展示没有完成的 todo 。
3. 点击 completed 状态，展示已完成的 todo 。

任务提示：

1. 定义 Vue.data.filter 状态为 all
2. 定义展示数据 showTodo ，更具 filter 的类型返回不同的数据
3. 点击导航切换 filter 的值

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/11.png?raw=true)

## 组件分离

任务要求：

1. 把页面拆分为 TheHeader、TodoList、TheFooter 三个部分

2. 分离后能正常使用

   ![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/12.png?raw=true)

   ![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/13.png?raw=true)
