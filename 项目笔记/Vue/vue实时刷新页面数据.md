[vue实时刷新页面数据 - 张新钢 - 博客园 (cnblogs.com)](https://www.cnblogs.com/zxg-code/p/13972696.html)

```
methods: { async getData () { const { data: res } = await this.$http.get('/data01') console.log(res) this.one = res console.log(this.one) }, // 定时器 timer () { return setTimeout(() => { this.getDataone() }, 1000) } },
```