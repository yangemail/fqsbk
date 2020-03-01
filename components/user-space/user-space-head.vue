<template>
	<!-- 背景图+用户基本信息 -->
	<view class="user-space-head u-f-ajc">
		<image :src="getBgImg" mode="widthFix" lazy-load @tap.stop="changeBgImg"></image>
		<view class="user-space-head-info u-f-ajc u-f-column">
			<image :src="userinfo.userpic" mode="widthFix"></image>
			<view class="user-space-margin u-f-ac">
				{{userinfo.username}}
				<tag-sex-age :sex="userinfo.sex" :age="userinfo.age"></tag-sex-age>
			</view>
			<view class="icon iconfont user-space-head-btn user-space-margin " :class="[isguanzhu?'active':'icon-zengjia']"
			 @tap.stop="guanzhu">{{!isguanzhu?'关注':'已关注'}}</view>
		</view>
	</view>

</template>

<script>
	// 性别+年龄组件
	import tagSexAge from "@/components/common/tag-sex-age.vue";

	export default {
		components: {
			tagSexAge,
		},
		props: {
			userinfo: Object,
		},
		data() {
			return {
				isguanzhu: this.userinfo.isguanzhu
			};
		},
		computed: {
			getBgImg() {
				return "../../static/bgimg/" + this.userinfo.bgimg + ".jpg"
			}
		},
		methods: {
			// 切换背景
			changeBgImg() {
				let picNum = parseInt(this.userinfo.bgimg);
				// console.log('---picNum: ' + picNum)
				this.userinfo.bgimg = picNum < 4 ? ++picNum : 1;
			},
			// 关注
			guanzhu() {
				this.isguanzhu = !this.isguanzhu;
			}
		},
	}
</script>

<style scoped>
	/* 公共间距 */
	.user-space-margin {
		margin: 15rpx 0;
	}

	.user-space-head {
		position: relative;
		height: 500rpx;
		/* overflow 属性规定当内容溢出元素框时发生的事情。hidden:内容会被修剪，并且其余内容是不可见的。 */
		overflow: hidden;
	}

	.user-space-head>image {
		width: 100%;
	}

	.user-space-head-info {
		position: absolute;
		top: 150rpx;
	}

	.user-space-head-info>image {
		width: 150rpx;
		height: 150rpx;
		border-radius: 100%;
	}

	.user-space-head-info>view:first-of-type {
		color: #FFF;
		font-size: 35rpx;
		font-weight: bold;
		/* text-shadow 属性向文本添加一个或多个阴影。text-shadow: h-shadow v-shadow blur color; */
		text-shadow: 2rpx 2rpx 10rpx #333;
	}

	.user-space-head-btn {
		background: #FFE933;
		color: #333;
		border: 1rpx solid #FFE933;
		padding: 0 15rpx;
		border-radius: 10rpx;
		font-size: 28rpx;
	}

	.active {
		background: none;
		color: #FFF;
		border: 1rpx solid #FFF;
	}
</style>
