<template>
	<view>
		<!-- 状态栏：使用状态栏进行占位，空出状态栏的位置 -->
		<uni-status-bar bgcolor="#FFE933"></uni-status-bar>
		<!-- 左上角的关闭按钮 -->
		<view class="icon iconfont icon-guanbi" @tap="back"></view>
		<!-- 引入背景图 -->
		<image class="loginhead" src="../../static/common/loginhead.png" mode="widthFix" lazy-load></image>
		<!-- 输入框+按钮 -->
		<view class="body">
			<!-- 输入昵称/手机号/邮箱、密码、登录，输入框和按钮登录 -->
			<template v-if="!status">
				<input type="text" class="uni-input common-input" placeholder="昵称/手机号/邮箱" v-model="username" />
				<view class="login-input-box">
					<input type="text" class="uni-input common-input forget-input" placeholder="请输入密码" v-model="password" />
					<view class="forget u-f-ajc loign-font-color">忘记密码</view>
				</view>
			</template>

			<!-- 手机验证码登录 -->
			<template v-else>
				<view class="login-input-box">
					<view class="phone u-f-ajc">+86</view>
					<input type="text" class="uni-input common-input phone-input" placeholder="手机号" v-model="phone" />
				</view>
				<view class="login-input-box">
					<input type="text" class="uni-input common-input forget-input" placeholder="请输入验证码" v-model="checknum" />
					<view class="forget u-f-ajc loign-font-color yanzhengma" @tap="getCheckNum">
						<view class="u-f-ajc">{{!codetime?'获取验证码':codetime+' s'}}</view>
					</view>
				</view>
			</template>

			<button type="primary" :loading="loading" class="user-set-btn" :class="{'user-set-btn-disable':disable}" @tap="submit"
			 :disabled="disable">登录</button>
		</view>
		<!-- 登录状态切换 -->
		<view class="login-status u-f-ajc login-padding login-font-color" @tap="changeStatus">
			{{status?'账号密码登录':'验证码登录'}}
			<view class="icon iconfont icon-jinru login-font-color"></view>
		</view>
		<!-- 第三方登录 -->
		<view class="other-login-title u-f-ajc login-padding login-font-color">第三方登录</view>
		<other-login></other-login>
		<!-- 协议 -->
		<view class="login-rule u-f-ajc login-padding login-font-color">
			注册即代表您同意<view>《XXX协议》</view>
		</view>
	</view>
</template>

<script>
	// 状态栏
	import uniStatusBar from "../../components/uni-status-bar/uni-status-bar.vue"
	// 第三方登录组件
	import otherLogin from "../../components/home/other-login.vue";

	export default {
		components: {
			uniStatusBar,
			otherLogin,
		},
		data() {
			return {
				status: false, //false：当前是账号密码登录； true：手机验证码登录
				disable: true,
				loading: false,
				username: "",
				password: "",
				phone: "",
				checknum: "",
				codetime: 0 ,// 验证码倒计时
		
			}
		},
		watch: {
			username(val) {
				this.onBtnChange();
			},
			password(val) {
				this.onBtnChange();
			},
			phone(val) {
				this.onBtnChange();
			},
			checknum(val) {
				this.onBtnChange();
			}
		},
		methods: {
			// 验证手机号码
			isPhoneNumValid() {
				let mPattern = /^1[34578]\d{9}$/;
				return mPattern.test(this.phone);
			},
			// 获取验证码
			getCheckNum() {
				if(this.codetime > 0) { // 正处于倒计时状态
					uni.showToast({
						title: '不能重复获取验证码',
						icon:"none"
					});
					return;
				}
				// 验证手机号码合法性
				if(!this.isPhoneNumValid()) {
					uni.showToast({
						title:"请输入正确的手机号码",
						icon:"none"
					});
					return;
				}
				
				// 请求服务器，让服务器发送验证码
				// 发送成功,开启倒计时
				this.codetime = 10;
				let timer = setInterval(()=>{
					this.codetime--;
					if(this.codetime == 0) {
						clearInterval(timer);
					}
				}, 1000);
			},
			// 初始化表单
			initInput() {
				this.username = ""
				this.password = ""
				this.phone = ""
				this.checknum = ""
			},
			// 改变按钮的状态
			onBtnChange() {
				if ((this.username && this.password) /*账号密码登录*/ || (this.phone && this.checknum) /*手机验证码登录*/ ) {
					this.disable = false;
					return;
				}
				this.disable = true;
			},
			// 切换登录状态
			changeStatus() {
				// 切换状态时,清空表单
				this.initInput()
				this.status = !this.status;
			},
			// 返回上一步
			back() {
				console.log("返回上一步");
			},
			// 提交登录 
			// TODO: 等讲到API接口的时候再进行讲述这部分逻辑
			submit() {
				// 账号密码登录
				if(!this.status){
					return;
				}
				// 验证码登录
				if(!this.isPhoneNumValid()) {
					uni.showToast({
						title: '请输入正确的手机号码',
						icon:"none"
					});
					return;
				}
				console.log("提交登录")
			}
		}
	}
</script>

<style>
	/* css 引入需要放到第一行 */
	@import url("../../common/form.css");

	.login-font-color {
		color: #BBBBBB;
	}

	.login-padding {
		padding: 20rpx 0;
	}


	.icon-guanbi {
		position: fixed;
		top: 60rpx;
		left: 30rpx;
		font-size: 40rpx;
		font-weight: bold;
		color: #332F0A;
		z-index: 100;
	}

	.loginhead {
		width: 100%;
	}

	.login-input-box {
		position: relative;
	}

	/* 定义.forget-input,如果不定义输入值的时候，光标和输入会藏到"忘记密码"的下面 */
	.login-input-box .forget-input {
		padding-right: 150rpx;
	}

	.login-input-box .forget,
	.login-input-box .phone {
		position: absolute;
		top: 0;
		height: 100%;
		z-index: 100;
		/* background: yellow; */
	}

	.login-input-box .forget {
		right: 0;
		/* 定义这个宽度是为了上面的.forget-input,不然不知道具体宽度需要多少 */
		width: 150rpx;
	}

	.login-input-box .phone {
		left: 0;
		width: 100rpx;
		font-weight: bold;
	}

	.login-input-box .phone-input {
		padding-left: 100rpx;
	}

	.yanzhengma>view {
		background: #EEEEEE;
		border-radius: 10rpx;
		font-size: 25rpx;
		width: 150rpx;
		padding: 10rpx 0;
	}

	.other-login-title {
		position: relative;
	}

	/* 在.other-login-title左边和右边分别增加。
	   :before是css中的一种伪元素，可用于在某个元素之前插入某些内容。
	   :after是css中的一种伪元素，可用于在某个元素之后插入某些内容。 */
	.other-login-title::before,
	.other-login-title::after {
		content: "";
		position: absolute;
		background: #BBBBBB;
		/* 高度为1rpx */
		height: 1rpx;
		/* 宽度为100rpx */
		width: 100rpx;
		/* 距离此元素的顶边50%位置 */
		top: 50%
	}

	.other-login-title::before {
		/* 距离屏幕的左边是25% */
		left: 25%;
	}

	.other-login-title::after {
		/* 距离屏幕的右边是25% */
		right: 25%;
	}
</style>
