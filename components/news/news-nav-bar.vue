<template>
	<view>
		<!-- 自定义导航栏，:fixed=true固定导航栏；:border="false"取出边框阴影 -->
		<uni-nav-bar :fixed="true" :statusBar="true" :border="false" @clickRight="openAdd">
			<!-- 左边 -->
			<block slot="left">
				<view class="nav-left">
					<view class="icon iconfont icon-qiandao"></view>
				</view>
			</block>
			<!-- 中间 -->
			<view class="nav-tab-bar u-f-ajc">
				<block v-for="(tab,index) in tabBars" :key="tab.id">
					<view class="u-f-ajc" :class="{'active':tabIndex == index}" @tap="changeTab(index)">
						{{tab.name}}
						<view v-if="(tabIndex == index)" class="nav-tab-bar-line"></view>
					</view>
				</block>
			</view>
			<!-- 右边 -->
			<block slot="right">
				<view class="nav-right u-f-ajfe">
					<view class="icon iconfont icon-bianji1"></view>
				</view>
			</block>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue";
	
	export default {
		components: {
			uniNavBar,
		},
		props: {
			tabBars: Array,
			tabIndex: Number,
		},
		data() {
			return {

			};
		},
		methods: {
			// 两个tab切换
			// changeTab(index) {
			// 	this.tabIndex = index;
			// },
			changeTab(index) {
				this.$emit("change-tab", index);
			},
			// 打开发布页面
			openAdd() {
				uni.navigateTo({
					url: "../add-input/add-input",
				});
			},
		},
	}
</script>

<style scoped>
	.nav-left>view,
	.nav-right>view {
		font-size: 22px;
	}

	.nav-left {
		margin-left: 5rpx;
	}

	.nav-left>view {
		color: #FF9619;
	}

	.nav-right {
		width: 100%;
	}

	.nav-tab-bar {
		/* border: 1rpx solid; */
		width: 100%;
		margin-left: -20rpx;
	}

	.nav-tab-bar>view {
		/* border: 1rpx solid; */
		font-size: 32rpx;
		font-weight: bold;
		color: #969696;
		padding: 0 15rpx;
	}

	.active {
		color: #333 !important;
	}

	.nav-tab-bar-line {
		border-bottom: 5rpx solid #FEDE33;
		border-top: 5rpx solid #FEDE33;
		width: 70rpx;
		border-radius: 20rpx;
		position: absolute;
		bottom: 12rpx;
	}
</style>
