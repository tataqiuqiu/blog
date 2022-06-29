---
title: vue 动态组件
date: 2022-6-27 11:00:00
tags: vue
categories:
  - javascript
  - vue
  - 组件
---

### 1、常用的引用组件方式
[例子链接](https://tataqiuqiu.github.io/demos/vue/test/dist/#/app-component-2)

``` html
<div>
  <ButtonCounter />
</div>
```
``` javascript
import ButtonCounter from "./ButtonCounter.vue"

export default {
  components: {
    ButtonCounter
  }
}
```

### 2、考虑如下场景
[例子链接](https://tataqiuqiu.github.io/demos/vue/test/dist/#/app-component)
``` html
<div>
  <button @click="CreateButtomCounter">点击加载组件</button>
  <div id="root"></div>
</div>
```

<!-- more -->

``` javascript
import { CreateButtomCounter } from "./CreateButtomCounter.js"

export default {
  methods: {
    CreateButtomCounter
  }
}
```

CreateButtomCounter.js
``` javascript
import Vue from "vue"
import ButtonCounter from "./ButtonCounter.vue"

export const CreateButtomCounter = () => {
  const ButtonCounterCom = Vue.extend(ButtonCounter)
  const instance = new ButtonCounterCom().$mount()  

  const dom = document.querySelector("#root")
  dom.appendChild(instance.$el)
}
```

### 3、Vue.extend()
[官方文档](https://cn.vuejs.org/v2/api/index.html#Vue-extend)
![](/images/vue-extend.png)

特点：只能通过自身初始化结构
使用范围：
（1）挂载在某元素下
（2）被vue实例的components引用
（3）Vue.component组件引用

### 4、Vue.component()
[官方文档](https://cn.vuejs.org/v2/api/index.html#Vue-component)
![](/images/vue-component.png)

特点：
（1）可通过自身初始化组件结构
（2）可通过引入vue.extend初始化组件结构
（3）可通过第三方模版temple.html初始化组件结构
使用范围： 任何已被vue初始化的元素内 [官方文档](https://cn.vuejs.org/v2/guide/components.html)

``` javascript 
<script>
//方法3 第三方模板引入
Vue.component('templecomponent', function(resolve, reject) {
  $.get("./../xtemplate/com.html").then(function(res) {
    resolve({
      template: res,
      props: ["b"],
      data: function() {
        return {
          a: "a"
        }
      }
    })
  })
})
</script>
```

### 5、new Vue
特点：
（1）可以通过自身components引用vue.extend构造，通过自身data向构造传参
（2）可以通过自身component引用组件模版，通过自身data向组件传参
使用范围：
（1）仅限于自身

``` html
<div id="app1">
	<dt1></dt1>
	<vueapple v-bind:b="msg"></vueapple>
</div>
```
``` javascript
<script type="text/x-template" id="dt1">
	<div>这里是子组件1</div>
</script>
```
``` javascript
<script>
	new Vue({
		el: "#app1",
		data: {
			msg: "vue实例参数"
		},
		components: {
			dt1: {
				template: "#dt1"
			},
			vueapple: Profile //【引入构造】
		}
	});
</script>
```

### 6、Vue.component() 与 Vue.extend() 关系
调用 Vue.component 时
1、调用 Vue.extend，即使用基础 Vue 构造器，创建一个“子类”。
2、注册全局组件 [官方文档](https://cn.vuejs.org/v2/guide/components.html)

如果是 new Vue 之后调用 Vue.component 呢？
以下代码等价

``` javascript
export const CreateButtomCounter = () => {
  const ButtonCounterCom = Vue.component('button-counter', ButtonCounter)
  const instance = new ButtonCounterCom().$mount()  

  const dom = document.querySelector("#root")
  dom.appendChild(instance.$el)
}
```
``` javascript
export const CreateButtomCounter = () => {
  const ButtonCounterCom = Vue.extend(ButtonCounter)
  const instance = new ButtonCounterCom().$mount()  

  const dom = document.querySelector("#root")
  dom.appendChild(instance.$el)
}
```

### 7、常用的引用组件方式 与 Vue.extend() 的关系


### 8、$mount()
$mount 方法支持传入 2 个参数，第一个是 el，它表示挂载的元素，可以是字符串，也可以是 DOM 对象，如果是字符串在浏览器环境下会调用 query 方法转换成 DOM 对象的。第二个参数是和服务端渲染相关，在浏览器环境下不需要传第二个参数。

``` javascript
const instance = new ButtonCounterCom().$mount()  

const dom = document.querySelector("#root")
dom.appendChild(instance.$el)
```
$mount()不带参数，会把组件在内存中渲染完毕
instance.$el 拿到的就是组件对应的dom元素,可以直接操作dom

### 9、经典案例
Vue.extend + $mount
[Dialog](https://element.eleme.io/#/zh-CN/component/dialog)
