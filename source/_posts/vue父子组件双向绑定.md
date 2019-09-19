---
title: vue父子组件双向绑定
date: 2019-8-5 11:00:00
tags: vue
categories:
  - javascript
  - vue
  - 组件
# demo: ../../../../../demo/vue/test.html
demo: https://tataqiuqiu.github.io/demos/vue/test/dist/#/bb
---

### 1、sync修饰符（v2.3.0+ 新增）

[父组件代码](https://github.com/tataqiuqiu/demos/blob/master/vue/test/src/views/Bb.vue)  

``` html
<div>
  <child :value.sync="doc"></child>
  <div>father： <input type="text" v-model="doc" /></div>
  <div>result： <span v-html="doc"></span></div>
</div>
```
``` javascript
import Child from "@/components/Bb-child.vue";
export default {
  name: "Bb",
  components: {
    Child
  },
  data() {
    return {
      doc: "输入试试"
    };
  }
};
```
<!-- more -->

[子组件代码](https://github.com/tataqiuqiu/demos/blob/master/vue/test/src/components/Bb-child.vue)

``` html
<div>
  <div>child： <input type="text" v-model="val" @input="iptInput" /></div>
</div>
```
``` javascript
export default {
  name: "Bb-child",
  props: {
    value: String
  },
  data() {
    return {
      val: this.value
    };
  },
  watch: {
    value(newVal) {
      this.val = newVal;
    }
  },
  methods: {
    iptInput() {
      this.$emit("update:value", this.val);
    }
  }
};
```

### 2、老版本

[父组件代码](https://github.com/tataqiuqiu/demos/blob/master/vue/test/src/views/Bb.2.vue)  

``` html
<div>
  <child :value="doc" @input="oninput"></child>
  <div>father： <input type="text" v-model="doc" /></div>
  <div>result： <span v-html="doc"></span></div>
</div>
```
``` javascript
import Child from "@/components/Bb-child.2.vue";
export default {
  name: "Bb",
  components: {
    Child
  },
  data() {
    return {
      doc: "输入试试"
    };
  },
  methods: {
    oninput(val) {
      this.doc = val;
    }
  }
};
```

[子组件代码](https://github.com/tataqiuqiu/demos/blob/master/vue/test/src/components/Bb-child.2.vue)
``` html
<div>child： <input type="text" v-model="val" @input="iptInput" /></div>
```
``` javascript
export default {
  name: "Bb-child.2",
  props: {
    value: String
  },
  data() {
    return {
      val: this.value
    };
  },
  watch: {
    value(newVal) {
      this.val = newVal;
    }
  },
  methods: {
    iptInput() {
      this.$emit("input", this.val);
    }
  }
};
```