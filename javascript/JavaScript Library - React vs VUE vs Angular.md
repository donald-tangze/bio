## [Vue.js 是什么](https://v2.cn.vuejs.org/v2/guide/index.html#Vue-js-是什么)

Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，

#### 1.**响应式** Reactive  

雙向綁定 (狀態和數據監聽)

每个 Vue 实例在被创建时都要经过一系列的初始化过程——例如，需要设置数据监听、编译模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。

![Vue 实例生命周期](https://v2.cn.vuejs.org/images/lifecycle.png)

#### 2.Template模板

Vue.js 使用了基于 HTML 的模板语法，允许开发者声明式地将 DOM 绑定至底层 Vue 实例的数据。所有 Vue.js 的模板都是合法的 HTML，所以能被遵循规范的浏览器和 HTML 解析器解析。

* 文本和HTML

  数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

```html
<span>Message: {{ msg }}</span>


```

* [指令](https://v2.cn.vuejs.org/v2/guide/syntax.html#指令)

指令 (Directives) 是带有 `v-` 前缀的特殊 attribute。指令 attribute 的值预期是**单个 JavaScript 表达式** (`v-for` 是例外情况，稍后我们再讨论)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。回顾我们在介绍中看到的例子：

```vue
<!-- v-if 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染。-->
<p v-if="seen">现在你看到我了</p>

<!-- v-on 指令监听 DOM 事件，并在触发时运行一些 JavaScript 代码。-->
<a v-on:click="doSomething">...</a> 

<a v-bind:href="url">...</a>
<a v-bind:[attributeName]="url"> ... </a>
```



#### 3.Declaritive, [声明式渲染](https://v2.cn.vuejs.org/v2/guide/index.html#声明式渲染)

主要是直接用在html中的Javascript標籤

```html
<div id="app">
  {{ message }}
</div>

<script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: '#app',
    data: {
      message: 'Hello Vue!'
    }
  })
</script>
```



#### 4.[Component](https://v2.cn.vuejs.org/v2/guide/components.html)

 [组件化应用构建](https://v2.cn.vuejs.org/v2/guide/index.html#组件化应用构建)

```html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

```html
<div id="app-7">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>

<scirpt>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
  
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: '蔬菜' },
      { id: 1, text: '奶酪' },
      { id: 2, text: '随便其它什么人吃的东西' }
    ]
  }
})
</scirpt>
```



## Angular 是什麼

Vue is simplified Angular.js

## Differences between Angular and AngularJS[[edit](https://en.wikipedia.org/w/index.php?title=Angular_(web_framework)&action=edit&section=1)]

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d1/Architecture_of_an_Angular_2_application.png/330px-Architecture_of_an_Angular_2_application.png)



Architecture of an Angular application. The main building blocks are modules, components, templates, metadata, data binding, directives, services, and dependency injection.

Google designed Angular as a ground-up rewrite of AngularJS.

- Angular does not have a concept of "scope" or controllers; instead, it uses a hierarchy of components as its primary architectural characteristic.[[5\]](https://en.wikipedia.org/wiki/Angular_(web_framework)#cite_note-5)
- Angular has a different expression syntax, focusing on `"[ ]"` for [property](https://en.wikipedia.org/wiki/Property_(programming)) binding, and `"( )"` for [event](https://en.wikipedia.org/wiki/Event_(computing)) binding[[6\]](https://en.wikipedia.org/wiki/Angular_(web_framework)#cite_note-6)
- Modularity – much core functionality has moved to modules
- Angular recommends the use ofMicrosoft's TypeScript language, which introduces the following features:
  - [Static typing](https://en.wikipedia.org/wiki/Static_typing), including [Generics](https://en.wikipedia.org/wiki/Generic_programming)
  - [Type annotations](https://en.wikipedia.org/wiki/Type_annotation)
- [Dynamic loading](https://en.wikipedia.org/wiki/Dynamic_loading)
- Asynchronous template compilations
- Iterative callbacks provided by RxJS.
- Support to run Angular applications on servers.

## [React.js 是什么](https://v2.cn.vuejs.org/v2/guide/index.html#Vue-js-是什么)

**React** (also known as **React.js** or **ReactJS**) is a [free and open-source](https://en.wikipedia.org/wiki/Free_and_open-source_software) [front-end](https://en.wikipedia.org/wiki/Frontend_and_backend) [JavaScript library](https://en.wikipedia.org/wiki/JavaScript_library)[[3\]](https://en.wikipedia.org/wiki/React_(software)#cite_note-react-3)[[4\]](https://en.wikipedia.org/wiki/React_(software)#cite_note-4) for building [user interfaces](https://en.wikipedia.org/wiki/User_interface) based on [components](https://en.wikipedia.org/wiki/Component-based_software_engineering). It is maintained by [Meta](https://en.wikipedia.org/wiki/Meta_Platforms) (formerly Facebook) and a community of individual developers and companies.

React can be used to develop [single-page](https://en.wikipedia.org/wiki/Single-page_application), mobile, or [server-rendered](https://en.wikipedia.org/wiki/Server-side_rendering) applications with frameworks like [Next.js](https://en.wikipedia.org/wiki/Next.js). Because React is only concerned with the user interface and rendering components to the [DOM](https://en.wikipedia.org/wiki/Document_Object_Model), React applications often rely on [libraries](https://en.wikipedia.org/wiki/JavaScript_libraries) for routing and other client-side functionality.

1.User Interface

2.Template

3.Component

4.Single Page Application