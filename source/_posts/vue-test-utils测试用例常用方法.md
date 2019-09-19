---
title: vue-test-utils测试用例常用方法
date: 2019-8-2 18:00:00
tags: vue-test-utils
categories:
  - javascript
  - vue
  - test-utils
---

测试用例，代码自动化监测，codereview的第一步。是个不应被忽视的环节。

<!-- more -->

``` javascript
import { mount } from '@vue/test-utils'
import test from '../index' // 引入组件
const wrapper = mount(test, {
  // 添加属性
  propsData: {
    type: 'type_1'
  },
  // 添加插片
  slots: {
    default: '<div class="test-msg"></div>'
  }
})
const vm = wrapper.vm // 组件实例

it('类名是否正确', () => {
  const container = wrapper.find('.container')
  expect(container.contains('.class_1')).toBe(true)
  expect(container.classes('class_2')).toBe(true)
})

it('触发click事件', () => {
  wrapper.trigger('click')
  expect(wrapper.emitted().click).toBeTruthy()
})

it('html内容检测', () => {
  const title = wrapper.find('.title')
  expect(title.text()).toBe('标题')

  const img = vm.$el.querySelector('.img')
  expect(img.src).toBe('http://img')
})

it('样式检测', () => {
  const vm = vm.$el
  expect(vm.style.width).toBe('300px')
})

it('开启检测', () => {
  expect(wrapper.contains('.detail')).toBe(true)
})

it('插片位置是否正确', () => {
  const minor = wrapper.find('.slot')
  expect(minor.contains('div.test-msg')).toBeTruthy()
})
```