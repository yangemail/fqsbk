<template>
	<view class="body">
		<input type="text" password class="uni-input common-input" placeholder="输入旧密码" v-model="oldpassword" />
		<input type="text" password class="uni-input common-input" placeholder="输入新密码" v-model="newpassword" />
		<input type="text" password class="uni-input common-input" placeholder="输入确认密码" v-model="renewpassword" />

		<button type="primary" :loading="loading" class="user-set-btn" :class="{'user-set-btn-disable':disable}" @tap="submit"
		 :disabled="disable">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				oldpassword: "",
				newpassword: "",
				renewpassword: "",
				loading: false,
				disable: true
			}
		},
		// 监听，确认是否三个input都已经有值了
		watch: {
			oldpassword(val) {
				this.change();
			},
			newpassword(val) {
				this.change();
			},
			renewpassword(val) {
				this.change();
			}
		},
		methods: {
			// 实时监听输入框
			change() {
				if (this.oldpassword && this.newpassword && this.renewpassword) {
					this.disable = false;
					return;
				}
				// 防止填写完之后，删除一个，则按钮不disable
				this.disable = true;
			},
			// 验证层
			check() {
				if (!this.oldpassword || this.oldpassword == "") {
					uni.showToast({
						title: "旧密码不能为空",
						icon: "none"
					});
					return false;
				}

				if (!this.newpassword || this.newpassword == "") {
					uni.showToast({
						title: "新密码不能为空",
						icon: "none"
					});
					return false;
				}

				if (!this.renewpassword || this.renewpassword == "") {
					uni.showToast({
						title: "重复输入新密码不能为空",
						icon: "none"
					});
					return false;
				}

				if (this.newpassword !== this.renewpassword) {
					uni.showToast({
						title: "确认密码和新密码不一致",
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
