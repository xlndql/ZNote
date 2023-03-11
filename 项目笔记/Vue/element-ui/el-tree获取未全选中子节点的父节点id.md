用getCheckedKeys()去获取所有选中节点的id，用getHalfCheckedKeys()去获取子节点未全选时的父节点id,然后将他们进行拼接，再传给后端接口，这样就不会完美解决了子节点未全选，父节点id获取不到的问题了。
```js
//提交权限分配 
submitAuth() { 
	if (this.activeName == "first") { 
		let parentArr = this.$refs.pageTree.getHalfCheckedKeys(); 
		//获取子节点未全选时的父节点id 
		let childArr = this.$refs.pageTree.getCheckedKeys(); 
		//获取所有选中节点的id 
		let permissionParams = { 
			//获取全选中的id
			permissionids:parentArr.concat(childArr), 
			//将两个数组进行拼接 
			roleid:this.editRoleId 
		} 
		$HTTP_updateRolePermission(permissionParams).then(res => { 
			if (res.code == 200 && res.data == true) { 
				this.$message({ type:"success", message:"更新成功" })
```