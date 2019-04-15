# vue_demo1.1学习笔记

## RUN

```
Vue Create vue_demo1.1
```

```
npm run serve
```

## NO.1配置文件

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/0.png?raw=true)

引入base.css	/	index.css	/	index.html	/并在App.vue中引入

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/2.png?raw=true)

成功引入后会显示

![](https://github.com/zhuayu/combat-todo/raw/master/todo.png)

接下来任务开始我们先把数据渲染上去使用到 

1. 在 Vue.data 中定义 todos，todo 包含 title、completed
2. 在 templete 中使用 for 绑定 todos 数据进行渲染

###### ![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/4.png?raw=true)

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



## 	列表修改绑定事件

![](https://github.com/xiaojilinggui/vue_demo1.1/blob/master/vue%E5%AD%A6%E4%B9%A0%E5%9B%BE%E7%89%87/6.png?raw=true)

## 列表绑定对应的方法

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
