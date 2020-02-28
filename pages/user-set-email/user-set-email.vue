<template>
	<view class="body">
		<input type="text" class="uni-input common-input" placeholder="输入需要绑定的邮箱" v-model="email" />
		<input type="text" password class="uni-input common-input" placeholder="请输入密码" v-model="password" />

		<button type="primary" :loading="loading" class="user-set-btn" :class="{'user-set-btn-disable':disable}" @tap="submit"
		 :disabled="disable">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				email: "",
				password: "",
				disable: true,
				loading: false
			}
		},
		watch:{
			email(val) {
				this.change()
			},
			password(val) {
				this.change()
			}
		},
		methods: {
			// 实时监听输入框
			change() {
				if (this.email && this.password) {
					this.disable = false;
					return;
				}
				// 防止填写完之后，删除一个，则按钮不disable
				this.disable = true;
			},
			// 验证层
			check() {
				if (!this.email|| this.email== "") {
					uni.showToast({
						title: "邮箱不能为空",
						icon: "none"
					});
					return false;
				}
				// 验证邮箱格式
				var ePattern = /^([A-Za-z0-9_\-\.])+\@([A-Za-z0-9_\-\.])+\.([A-Za-z]{2,4})$/;
				if(!ePattern.test(this.email)) {
					uni.showToast({
						title:"邮箱格式错误",
						icon:"none"
					});
					return false;
				}

				if (!this.password || this.password== "") {
					uni.showToast({
						title: "密码不能为空",
						icon: "none"
					});
					return false;
				}

				return true;
			},
			// 提交
			submit() {
				// 提交状态
				this.loading = true;
				// disable这个按钮
				this.disable = true;

				if (!this.check()) {
					this.loading = false;
					this.disable = false;
					return;
				}

				setTimeout(() => {
					this.loading = false;
					this.disable = false;

					uni.showToast({
						title: "提交服务器",
						mask: false,
						duration: 1500
					});
				}, 2000);
			}
		}
	}
</script>

<style>
	/* css 引入需要放到第一行 */
	@import url("../../common/form.css");
</style>
