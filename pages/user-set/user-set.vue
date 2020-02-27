<template>
	<view class="body">
		<block v-for="(item, index) in list" :key="index">
			<home-list-item :item="item" :index="index"></home-list-item>
		</block>
		<button type="primary" class="user-set-btn">退出登录</button>
	</view>
</template>

<script>
	import homeListItem from "../../components/home/home-list-item.vue"

	export default {
		components: {
			homeListItem,
		},
		data() {
			return {
				// 功能列表
				list: [{
						icon: "",
						name: "账号与安全",
						clicktype: "navigateTo",
						url: "../user-set-repassword/user-set-repassword"
					}, {
						icon: "",
						name: "绑定邮箱",
						clicktype: "",
						url: ""
					}, {
						icon: "",
						name: "资料编辑",
						clicktype: "",
						url: ""
					},
					{
						icon: "",
						name: "小纸条",
						clicktype: "",
						url: ""
					}, {
						icon: "",
						name: "清除缓存",
						clicktype: "",
						url: ""
					}, {
						icon: "",
						name: "意见反馈",
						clicktype: "",
						url: ""
					}, {
						icon: "",
						name: "关于仿糗百",
						clicktype: "",
						url: ""
					}
				]
			}
		},
		methods: {
		}
	}
</script>

<style>
	.body {
		padding: 0 20rpx;
	}

	.user-set-btn {
		width: 100%;
		margin: 20rpx 0;
		background-color: #FFE933;
		border: 0 !important;
		color: #333;
	}
</style>
