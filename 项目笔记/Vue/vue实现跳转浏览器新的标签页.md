[(101条消息) vue实现跳转浏览器新的标签页_姜无忧的博客-CSDN博客_vue跳转新页面开新窗口](https://blog.csdn.net/xiasohuai/article/details/81777198?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-4-81777198-blog-125150582.pc_relevant_aa&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-4-81777198-blog-125150582.pc_relevant_aa)

```js
let newpage = this.$router.resolve({ 
	name: 'messageInfo', 
	query:{ 
		objectType:1, 
		infoId:id 
	} 
}) 
window.open(newpage.href, '_blank');
```