[(95条消息) Vue实现tab页多页面切换_皮蛋solo周呀的博客-CSDN博客_vue切换页面](https://blog.csdn.net/weixin_44590591/article/details/124866869?spm=1001.2101.3001.6650.8&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-8-124866869-blog-120182616.pc_relevant_multi_platform_whitelistv1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-8-124866869-blog-120182616.pc_relevant_multi_platform_whitelistv1)

VueX记录下每次新增后的tab标签页路由

store.js

```js
import Vue from 'vue'
import Vuex from 'vuex' 

Vue.use(Vuex) 

export default new Vuex.Store({ 
	state: { 
	// 路由导航start 
	// 缓存组件页面 
	catch_components: [], 
	// 当前选中的菜单 - 默认选择首页 
	activePath: '/index', 
	// 菜单项 - 默认需要展示的页面() 
	tabList: [{ 
		path: '/index', 
		label: '首页', 
		name: 'index', 
		fullPath: "/index" 
		}], 
		// 路由导航end 
	}, 
	// 更改vuex的store中状态的唯一方法 - 同步操作 
	mutations: { 
	// 路由导航start 
	//清空vuex数据 
	clearVUEX(state) { 
		state.catch_components = [] 
		state.activePath = 'index' 
		state.tabList = [{ 
		path: '/idnex', 
		label: '首页', 
		name: 'index', 
		fullPath: "/index" 
		}] 
	}, 
	// 跳转页面执行 
	selectMenu(state, submenu) { 
	// 首页就是 wellcome 也就是 home 
	if (submenu.name === 'index') {
		submenu.name = 'index' 
		label.path = '首页' 
		submenu.path = '/index' 
		submenu.fullPath= '/index' 
	} 
	// 当前选中菜单 
	var activePath = submenu.name 
	// 历史已选中菜单列表 
	var oldTabList = state.tabList 
	// 将菜单信息添加到tablist - 添加时判断是否已有该路由标签 
	var result = oldTabList.some(item => { 
		if (item.name === activePath) { 
		// console.log('--------', item.fullPath != submenu.fullPath) 
		// 有该路由标签是否为多次点击(相当于查看同路由下的详情，该过程只改变了参数) 
			if (!item.fullPath != submenu.fullPath) {
				item.fullPath = submenu.fullPath 
			} 
			return true 
		} 
	}) 
	// 如果不包含该对象，则添加 
	if (!result) { 
		oldTabList.push({ 
			path: submenu.name, 
			name: submenu.name, 
			label: submenu.label, 
			fullPath: submenu.fullPath 
		})
	} 
	// 重新赋值标签路由和当前选中菜单 
	state.activePath = activePath 
	state.tabList = oldTabList 
	}, 
	// 添加keepalive缓存 
	addKeepAliveCache(state, val) { 
		// 如果是首页不缓存 
		if (val === 'index') { 
			return 
		} 
		// console.log(state.catch_components) 
		// 添加时判断，如果该组件已存在，便不添加 
		if (state.catch_components.indexOf(val) === -1) { 
			// 不存在，缓存页面
			 state.catch_components.push(val) 
		} 
	}, 
	// 删除keepalive缓存 
	removeKeepAliveCache(state, val) { 
		let cache = state.catch_components 
		for (let i = 0; i < cache.length; i++) { 
			if (cache[i] === val) { 
				cache.splice(i, 1); 
			} 
		} 
		state.catch_components = cache 
	}, 
	//关闭菜单 
	closeTab(state, val) { 
		// 重新赋值 
		state.activePath = val.activePath
		state.tabList = val.tabList 
	}, 
	// 点击标签选择菜单 
	changeMenu(state, val) { 
		state.activePath = val 
	}, 
	// 路由导航end 
	}, 
	actions: {
	} 
})
```

若F5或者强刷新页面时需要保留当前tab路由数据，在App.vue中插入代码

```
created() { //在页面刷新时将vuex里的信息保存到sessionStorage里 window.addEventListener("beforeunload", () => { sessionStorage.setItem("store", JSON.stringify(this.$store.state)) }) },
```