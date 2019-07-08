---
title: Vue.js中方法与事件处理器
date: 2016-10-30 20:37:12
tags: Vue.js
---


## 一.方法处理器

可以用 v-on 指令监听 DOM 事件：

    //.html
    <div id="example">
      <button v-on:click="greet">Greet</button>
    </div>
    
我们绑定了一个单击事件处理器到一个方法 greet。下面在 Vue 实例中定义这个方法：

    var vm = new Vue({
      el: '#example',
      data: {
        name: 'Vue.js'
      },
      //在methods对象中定义方法
      methods: {
        greet: function (event) {
          //方法内this指向vm
          alert('Hello ' + this.name + '!')
          //event是原DOM事件
          alert(event.target.tagName)
        }
      }
    })

    // 也可以在 JavaScript 代码中调用方法
    vm.greet() // -> 'Hello Vue.js!'

## 二.内联语句处理器

除了直接绑定到一个方法，也可以用内联 JavaScript 语句：

    
    //.html
    <div id="example-2">
      <button v-on:click="say('hi')">Say Hi</button>
      <button v-on:click="say('what')">Say What</button>
    </div>
    

    //.js
    var vm = new Vue({
      el: '#example-2',
      methods: {
        say: function (msg) {
          alert(msg)
        }
      }
    }) 
    
result:

    Hi

    What
    
## 三.事件修饰符

在事件处理器中经常需要调用 event.preventDefault() 或 event.stopPropagation()。尽管我们在方法内可以轻松做到，不过让方法是纯粹的数据逻辑而不处理 DOM 事件细节会更好。

为了解决这个问题，Vue.js 为 v-on 提供两个 事件修饰符：.prevent 与 .stop。

    <!-- 阻止单击事件冒泡 -->
    <a v-on:click.stop="doThis"></a>

    <!-- 提交事件不再重载页面 -->
    <form v-on:submit.prevent="onSubmit"></form>

    <!-- 修饰符可以串联 -->
    <a v-on:click.stop.prevent="doThat">
    
    <!-- 只有修饰符 -->
    <form v-on:submit.prevent></form>
    
## 四.按键修饰符

在监听键盘事件时，我们经常需要检测 keyCode。Vue.js 允许为 v-on 添加按键修饰符：

    <!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
    <input v-on:keyup.13="submit">
    
记住所有的 keyCode 比较困难，Vue.js 为最常用的按键提供别名：

    <!-- 同上 -->
    <input v-on:keyup.enter="submit">

    <!-- 缩写语法 -->
    <input @keyup.enter="submit">
    
## 五.为什么在 HTML 中监听事件?

你可能注意到这种事件监听的方式违背了传统理念 “separation of concern”。不必担心，因为所有的 Vue.js 事件处理方法和表达式都严格绑定在当前视图的 ViewModel 上，它不会导致任何维护困难。实际上，使用 v-on 有几个好处：

1. 扫一眼 HTML 模板便能轻松定位在 JavaScript 代码里对应的方法。

2. 因为你无须在 JavaScript 里手动绑定事件，你的 ViewModel 代码可以是非常纯粹的逻辑，和 DOM 完全解耦，更易于测试。

3. 当一个 ViewModel 被销毁时，所有的事件处理器都会自动被删除。你无须担心如何自己清理它们。