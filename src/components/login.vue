<template>
	<div class="login_container">
		<div class="login_box">
			<div class="avatar_box">
				<img src="../assets/logo.png" />
			</div>
			<el-form label-width="0px" class="login_form" :model="loginForm" :rules="loginFormRules" ref="loginFormRef">
				<el-form-item prop="username">
					<el-input v-model="loginForm.username" prefix-icon="el-icon-user"></el-input>
				</el-form-item>

				<el-form-item prop="password">
					<el-input v-model="loginForm.password" type="password" prefix-icon="el-icon-lock"></el-input>
				</el-form-item>

				<el-form-item class="btns">
					<el-button type="primary" @click="loginFormValidate">登录</el-button>
					<el-button type="infor" @click="loginFormReset">重置</el-button>
				</el-form-item>

			</el-form>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				loginForm: {
					username: "admin",
					password: "admin"
				},
				loginFormRules: {
					username: [{
							required: true,
							message: '请输入用户名称',
							trigger: 'blur'
						},
						{
							min: 3,
							max: 20,
							message: '长度在 3 到 20 个字符',
							trigger: 'blur'
						}
					],
					password: [{
							required: true,
							message: '请输入密码',
							trigger: 'blur'
						},
						{
							min: 6,
							max: 16,
							message: '长度在 6 到 16 个字符',
							trigger: 'blur'
						}
					]
				}
			}
		},
		methods: {
			loginFormReset() {
				console.log(this);
				this.$refs.loginFormRef.resetFields();
			},
			loginFormValidate() {
				this.$refs.loginFormRef.validate(valid => {
					console.log(valid);
					if (!valid) return;
					//发送请求获取token
					/*
					const res = this.$http.post('login.do', this.loginForm);
					console.log(res);
					*/
					if (this.loginForm.username == "admin" && this.loginForm.password == "admin123") {
						const token = "12312312312312312";
						window.sessionStorage.setItem("token", token);
						this.$message.success("登陆成功");
						this.$router.push("/home");
					} else {
						this.$message.error("登陆失败");
					}

				})
			}
		}
	}
</script>

<style lang="less" scoped="scoped">
	.login_container {
		height: 100%;
		background-color: #2b4b6b;
	}

	.login_box {
		width: 450px;
		height: 300px;
		background-color: #fff;
		border-radius: 3px;
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);

		.avatar_box {
			height: 130px;
			width: 130px;
			border: 1px solid #eee;
			border-radius: 50%;
			padding: 10px;
			box-shadow: 0 0 10px #ddd;
			position: absolute;
			left: 50%;
			transform: translate(-50%, -50%);
			background-color: #fff;

			img {
				width: 100%;
				height: 100%;
				border-radius: 50%;
				background-color: #eee;
			}
		}
	}

	.login_form {
		position: absolute;
		bottom: 0;
		width: 100%;
		padding: 0 20px;
		box-sizing: border-box;
	}

	.btns {
		display: flex;
		justify-content: flex-end;
	}
</style>
