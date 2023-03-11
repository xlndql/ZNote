```shell
npm install mavon-editor -S
```

```js
// main.js 全局注册 
import mavonEditor from 'mavon-editor' 
import 'mavon-editor/dist/css/index.css' 
// use 
Vue.use(mavonEditor)
```

Vue 页面使用

```vue
<div> 
	<mavon-editor ref="md" v-model="value" :ishljs="true" @imgAdd="imgAdd" /> 
</div> 
<!-- 预览 --> 
<mavon-editor 
	class="md"
	:value="article.content" 
	:subfield="false" 
	:default-open="'preview'" 
	:toolbars-flag="false" 
	:scroll-style="true" 
	:ishljs="true" 
/> 
// 绑定imgAdd event 
imgAdd(pos,$file) { 
	let $vm = this.$refs.md 
	// 第一步，将图片上传到服务器 
	const formData = new FormData() 
	formData.append('file',$file) 
	axios({ 
		url: '', 
		method: 'post', 
		data: formData, 
		headers: {
			'Content-Type': 'multipart/form-data'}, }).then((res) => { // 第二步，将返回的url替换到文本原位置 ![...](./0) -> ![...](url) $vm.$img2Url(pos,res.data) }) },
```