[(100条消息) 【Vue-router】解决父级路由不需要 component的情况_songywaa的博客-CSDN博客](https://blog.csdn.net/weixin_42288182/article/details/115176711)

解决办法

将component 写成component: {render: (e) => e("router-view")}