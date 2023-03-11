[mavon-editor 自定义工具栏按钮，实现文件上传功能(或其他自定义功能)。 - 简书 (jianshu.com)](https://www.jianshu.com/p/381f7f4d8ad9)

显示图标：

```js
<mavon-editor 
	ref="md" 
	v-model="newValue" 
> 
	<!-- 通过插槽将我们的icon插入到工具栏中 下面给出四个插槽名，大家可以自行更换--> 
	<!-- left-toolbar-before --> 
	<!-- left-toolbar-after --> 
	<!-- right-toolbar-before --> 
	<!-- right-toolbar-after --> 
	<template v-slot:left-toolbar-after> 
		<button 
			type="button" 
			title="文件上传" 
			class="op-icon fa markdown-upload iconfont iconupload" 
			aria-hidden="true" 
			@click="uploadFile" 
		> 		
			<!-- 这里用的是element-ui给出的图标 --> 
			<i class="el-icon-upload"/> 
		</button> 
	</template> 
</mavon-editor> 
<!-- 在这里放一个隐藏的input，用来选择文件 --> 
<input ref="uploadInput" style="display: none" type="file" @change="uploadFileChange">
```

接口代码：

// 这是我们自定义的按钮触发的方法，这里也可以在自定义其他功能时做一些其他操作。 uploadFile() { // 通过ref找到隐藏的input标签，触发它的点击方法 this.$refs.uploadInput.click() }, // 监听input获取文件的状态 uploadFileChange(e) { // 获取到input选取的文件 const file = e.target.files[0] // 创建form格式的数据，将文件放入form中，logo是与后台定义的字段 const formdata = new FormData() formdata.append('logo', file) // 发送请求，这里是大家各自的axios请求，方法大家按照各自项目更换就好啦 axios.post('/upload',formdata).then(res => { // 这里获取到的是mavon编辑器实例，上面挂载着很多方法 const $vm = this.$refs.md // 将文件名与文件路径插入当前光标位置，这是mavon-editor 内置的方法 $vm.insertText($vm.getTextareaDom(), { prefix: `[${file.name}](${res.data.path})`, subfix: '', str: '' }) }) },