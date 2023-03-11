[(95条消息) 使用路由守卫 + vuex实现前端路由权限控制_qq_42373684的博客-CSDN博客](https://blog.csdn.net/qq_42373684/article/details/105959048)

# vue + vuex实现路由权限控制

## 一、定义权限路由

在路由中通过meta.role定义能访问该路由的权限组

router/index.js

``` js
import Home from '@views/home' 
import Test1 from '@views/test1' 
import Test2 from '@views/test2' 
import Test3 from '@views/test3' 
// 所有路由 
export const all = [ 
	{
		path: '/', 
		name: 'home', 
		component: Home, 
		meta: { 
			title: '首页', 
			role: ['admin', 'group_admin', 'user'] 
		} 
	}, 
	{ 
		path: '/test1', 
		name: 'test1', 
		component: Test1,
		meta: { 
			title: '测试1', 
			role: ['admin'] 
		} 
	}, 
	{ 
		path: '/test2', 
		name: 'test2', 
		component: Test2, 
		meta: { 
			title: '测试2', 
			role: ['admin', 'group_admin'] 
		} 
	},
	{ 
		path: '/test3', 
		name: 'test3', 
		component: Test3,
		meta: { 
			title: '测试3', 
			role: ['admin', 'user'] 
		} 
	} 
] 

let router = new Router({routes: all}) 

export default router
```

## 二、vuex

index.js

```js
import Vue from 'vue'; 
import Vuex from 'vuex'; 
import * as getters from './getters' 
import * as actions from './actions' 
import * as mutations from './mutations' 
Vue.use(Vuex); 
const state = {
	userRole: '', 
	isPowerful: false, 
}; 
// 注册上面引入的各大模块 
const store = new Vuex.Store({ 
	state, // 共同维护的一个状态，state里面可以是很多个全局状态 
	getters, // 获取数据并渲染 
	mutations, // 数据的异步操作 
	actions, // 处理数据的唯一途径，state的改变或赋值只能在这里 
}) ;
export default store;
```

actions.js

注：异步方法只能在actions中使用

```js
import axios from 'axios' 
import {all} from '@/router' 

function get(url, params, config) { 
	return new Promise((resolve, reject) => { 
		axios.get(url, { 
			params: params, 
			config: config 
		})
		.then(res => { resolve(res) })
		.catch(err => { reject(err) })
	}) 
} 

// 给action注册事件处理函数。当这个函数被触发时候，将状态提交到mutations中处理 
export async function getUserRole({commit}, userRole) { 
	// 请求登录接口获取登录用户身份，返回值与接口相关，可根据自己的接口再次调整 
	await get('/login_info').then(res => { userRole = res.data.user_role }) 
	// 第一个参数为提交的mutations中的方法名 
	return commit('getUserRole', userRole) 
} 

export async function confirmUserPower({commit}, data) { 
	for (let i = 0; i < all.length; i++) { 
		if (data.to.path === all[i].path && (all[i]['meta'].role.indexOf(data.userRole) > -1)) { 
		// 若当前用户在权限组中，设置isPowerful为true 
			data.isPowerful = true 
			break 
		} else { 
			data.isPowerful = false 
		} 
	} 
	return commit('confirmUserPower', data) 
}
```

mutations.js

```js
// 提交 mutations是更改Vuex状态的唯一合法方法 
export const getUserRole = (state, userRole) => { 
	state.userRole = userRole 
} 
export const confirmUserPower = (state, data) => { 
	state.isPowerful = data.isPowerful 
}
```

三、路由守卫

router/index.js

```js
router.beforeEach(async (to, from, next) => { 
	// 第一次登录成功时获取userRole 
	if (store.state.userRole === '') { 
		await store.dispatch('getUserRole') 
	} 
	let data = {
		'to': to, 
		'userRole': store.state.userRole, 
		isPowerful: ''
	} 
	await store.dispatch('confirmUserPower', data) 
	if (to.matched.length === 0) { 
	// 没有相应路由无法跳转，返回至当前页面或首页 
	from.path ? next({path: from.path}) : next('/'); 
	} else if (store.state.isPowerful) {
	// 路由存在且有权限才能跳转至相应路由页面 next(); } else { // 路由存在且无权限不能跳转，返回至当前页面或首页 from.path ? next({path: from.path}) : next('/'); } });
```