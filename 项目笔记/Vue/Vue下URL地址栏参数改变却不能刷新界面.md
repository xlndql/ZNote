[(102条消息) Vue下URL地址栏参数改变却不能刷新界面_夏已微凉、的博客-CSDN博客_vue地址栏变化但页面没反应](https://lrbbfc.blog.csdn.net/article/details/124891499?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-124891499-blog-116754948.pc_relevant_multi_platform_whitelistv3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-124891499-blog-116754948.pc_relevant_multi_platform_whitelistv3)

```js
<script> 
import axios from 'axios' 
export default { 
	data() { 
		return { 
			list: [], 
			hobby: 'study' 
		} 
	}, 
	mounted() { 
		this.getHobby(this.hobby); //调用爱好获取方法 
	}, 
	watch: { 
		'$route' (to, from) { 
			//监听URL地址栏参数变化 
			let queryHobby = this.$route.query.hobby; 
			if (queryHobby) { 
				this.getHobby(queryHobby) 
			} 
		} 
	}, 
	methods: { 
		getHobby(hobby) { 
		//接口获取爱好数据 
			axios({ 
				url: 'http://***.com/hobby/lists',
				method: 'GET', 
				params: {hobby: hobby} 
			}).then(res => { this.list = res.data.data; 
			//获取接口中的数据，并赋值 
			}) 
		} 
	} 
} 
</script>
```