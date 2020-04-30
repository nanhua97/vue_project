<template>
	<div>
		登陆成功
		<el-button type="info" @click="loginOut">退出</el-button>
	</div>
</template>

<script>
	export default {
		data() {
			return {}
		},
		methods: {
			loginOut() {
				window.sessionStorage.clear();
				this.$router.push("/login");
			}
		}
	}
</script>

<style>
</style>
