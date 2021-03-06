# vue-cli

## 访问public文件夹

1）描述

任何放置在public文件夹的静态资源都会被简单复制，而不经过webpcak.需要通过绝对路径来引用他们。

2）在public/index.html 或其他通过 html-webpack-plugin用作模板的HTML文件中，需要通过<%= BASE_URL %>设置链接前缀：

```html
<link rel="icon" href="<%= BASE_URL %>favicon.ico">
```

3）在模板中，你首先需要向你的组件传入基础URL:

```JS
data(){
    return{
        publicPath: process.env.BASE_URL
    }
}
然后：
<img :src="`${publicPath}my-image.png`">
```

4）在 sass 中使用

```css
.bg{
	background: url('/img/mini-bg.png');
	// '/' 表示根路径，此路径是在 public/img 下
}
```

## 引入src/assets图片

### 使用相对路径引入

```
 <img src="../assets/images/temp_1_1.png" alt="">
```

### 使用 require

```
require('@/assets/images/demo.png')
```

## 设置浏览器标题

### 页面设置标题相同

```
<head>
	<title>我是标题</title>
</head>
```

### 页面设置标题不同

```
router - index.js

// 路由中定义路由元信息
const router = new Router({
	routes: [
		{
			path: 'index',
			meta:{
				title: '首页' //在此处设置标题
			}
		}
	]
})

// 在路由的全局前置守卫进行拦截
main.js

router.beforeEach((to, from, next) =>{
	document.title = to.meta.title
})

```

