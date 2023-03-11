解决办法：

1、如果你在mounted里获取this.$refs，因为dom还未完全加载，所以你是拿不到的， update阶段则是完成了数据更新到 DOM 的阶段(对加载回来的数据进行处理)，此时，就可以使用this.$refs了

2、如果写在method中，那么可以使用 this.$nextTick(() => {}) 等页面渲染好再调用，这样就可以了

3、或者加个定时器延时加载this.$refs（这个方法还没有试）