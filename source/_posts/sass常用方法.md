---
title: sass常用方法
date: 2019-9-20 16:30:00
tags: sass
categories:
  - css
  - sass
---

## 一、控制指令: 

### 1、@for 循环

@for $var from &lt;start&gt; through &lt;end&gt;

@for $var from &lt;start&gt; to &lt;end&gt;

当使用 through 时，条件范围包含 &lt;start&gt; 与 &lt;end&gt; 的值，而使用 to 时条件范围只包含 &lt;start&gt; 的值不包含 &lt;end&gt; 的值

``` css
@for $i from 1 through 3 {
  .item-#{$i} {
    transform: rotate(($i * 30) * 1deg);
    animation: load 1.2s linear (($i - 1) / 10) * 1s infinite;
  }
}
```

<!-- more -->

编译后

``` css
.item-1 {
  transform: rotate(30deg);
  animation: load 1.2s linear 0s infinite;
}
.item-2 {
  transform: rotate(60deg);
  animation: load 1.2s linear 0.1s infinite;
}
.item-3 {
  transform: rotate(90deg);
  animation: load 1.2s linear 0.2s infinite;
}
```