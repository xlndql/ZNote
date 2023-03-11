Redirected when going from “/xxx“ to “/xxxxx“ via a navigation guard.

全局解决：替换路由的Push和replace方法，放在src/router/index.js中：

```js
import Router from 'vue-router' 

const originalPush = Router.prototype.push 
Router.prototype.push = function push(location, onResolve, onReject) { 
	if (onResolve || onReject) 
		return originalPush.call(this, location, onResolve, onReject) 
	return originalPush.call(this, location).catch(err => err) 
}
```