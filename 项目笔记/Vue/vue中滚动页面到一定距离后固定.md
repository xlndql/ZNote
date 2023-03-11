[(101条消息) vue中滚动页面到一定距离后固定_兮夏-的博客-CSDN博客_vue滚动到一定位置后固定显示](https://blog.csdn.net/m0_46693606/article/details/124124672)

1.id名为testNavBar的盒子与:class=’{ fixedNavbar: isfixTab }'的盒子可以是包含关系也可以是并列关系

```html
<div :class="{'fixedNavbar':isfixTab}">
```

2.fixedNavbar是类名

```js
.fixedNavbar { 
	position: fixed; 
}
```

3.isfixTab 是控制是否加类名

```js
data() { 
	return { 
		isfixTab:false 
	} 
},
```

4.在mounted中监听页面滚动事件,并调用handleTabFix() 方法

// 监听页面滚动 mounted () { window.addEventListener('scroll', this.handleTabFix, true) }, //离开当前组件前一定要清除滚动监听，否则进入其他路由会报错 beforeRouteLeave (to, from, next) { window.removeEventListener('scroll', this.handleTabFix, true) next() },

5.声明一个方法handleTabFix()

// 先分别获得id为testNavBar的元素距离顶部的距离和页面滚动的距离 // 比较他们的大小来确定是否添加fixedNavbar样式 handleTabFix() { var scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop var offsetTop = document.querySelector('#testNavBar').offsetTop scrollTop > offsetTop ? this.isfixTab = true : this.isfixTab = false }