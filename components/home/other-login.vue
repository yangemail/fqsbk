<template>
	<!-- 第三方登录 -->
	<view class="other-login u-f-ac">
		<block v-for="(item, index) in providerList" :key="index">
			<view class="u-f-ajc u-f1" @tap="tologin(item)">
				<view class="icon iconfont u-f-ajc" :class="['icon-'+item.icon ]"></view>
			</view>
		</block>
		<!-- <view class="u-f-ajc u-f1">
			<view class="icon iconfont icon-weixin u-f-ajc"></view>
		</view>
		<view class="u-f-ajc u-f1">
			<view class="icon iconfont icon-xinlangweibo u-f-ajc"></view>
		</view>
		<view class="u-f-ajc u-f1">
			<view class="icon iconfont icon-QQ u-f-ajc"></view>
		</view> -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				providerList: []
			};
		},
		onLoad() {
			console.log('--- onLoad() method is called. ---');
		},
		// 在组件中并不能使用页面生命周期函数，所以我直接将onLoad换成mounted。
		mounted() {
			console.log('--- mounted() method is called. ---');
			this.getLoginAuth();
		},
		methods: {
			// 获取当前登录渠道
			getLoginAuth() {
				uni.getProvider({
					service: 'oauth',
					success: (result) => {
						console.log('--- result --- : ' + JSON.stringify(result))
						
						this.providerList = result.provider.map((value) => {
							let providerName = '';
							let icon = '';
							switch (value) {
								case 'weixin':
									providerName = '微信登录'
									icon = 'weixin';
									break;
								case 'qq':
									providerName = 'QQ登录'
									icon = 'QQ';
									break;
								case 'sinaweibo':
									providerName = '新浪微博登录'
									icon = 'xinlangweibo';
									break;
								case 'alipay':
									providerName = '支付宝登录';
									icon = '';
									break;
							}
							return {
								name: providerName,
								icon: icon,
								id: value
							}
						});
				
					},
					fail: (error) => {
						console.log('获取登录通道失败', error);
					}
				});
			},
			// 登录
			tologin(provider) {
				uni.login({
					provider: provider.id,
			        // #ifdef MP-ALIPAY
			        scopes: 'auth_user',  //支付宝小程序需设置授权类型
			        // #endif
					success: (res) => {
						console.log(JSON.stringify(res));
						console.log('login success:', res);
						// 更新保存在 store 中的登录状态
						console.log('登陆成功，保存到本地存储，修改当前用户登录状态。');
					},
					fail: (err) => {
						console.log('login fail:', err);
					}
				});
			}
		},
	}
</script>

<style scoped>
	.other-login {
		padding: 20rpx 80rpx;
	}

	.other-login>view>view {
		width: 100rpx;
		height: 100rpx;
		/* border: 1rpx solid; */
		border-radius: 100%;
		font-size: 55rpx;
		color: #FFF;
	}

	.other-login .icon-QQ {
		background-color: #2CAEFC;
	}

	.other-login .icon-weixin {
		background-color: #2BD19B;
	}

	.other-login .icon-xinlangweibo {
		background-color: #FC7729;
	}
</style>
