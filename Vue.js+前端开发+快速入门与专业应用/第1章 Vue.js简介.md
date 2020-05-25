# 第一章 Vue.js简介
## 1.1 　Vue.js的Hello world
引入 Vue.js ，使用 CDN

```html
<script src='http://cdnjs.cloudflare.com/ajax/libs/vue/1.0.26/vue.min.js'></script>
```

也可以通过 NPM 进行安装：

```cmd
npm install vue // 最新稳定版本
```

正确引入 Vue.js 之后，我们在 HTML 文件中的内容为：

```html
<div id="app">
    <h1>{{message}}</h1>
</div>
```

应用的 js 如下：

```js
var vm = new Vue({
	el : '#app',
	data: {
　　	message : 'Hello world, I am Vue.js'
	}
});
```

输出结果为：

![](E:\MarkDown\Vue.js+前端开发+快速入门与专业应用\图床\helloworld.png)

