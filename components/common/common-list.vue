<template>
	<!-- 使用在关注页面 -->
	<!-- 动态列表组件 -->
	<view class="common-list u-f animated fadeInLeft fast">
		<!-- 左侧头像 -->
		<view class="common-list-left">
			<image :src="item.userpic" mode="widthFix" lazy-load></image>
		</view>
		<!-- 右侧内容 -->
		<view class="common-list-right">
			<!-- 右边分为4行 -->
			<!-- 第1行 -->
			<view class="u-f-ac u-f-jsb">
				<view class="u-f-ac">{{item.username}}
					<!-- 性别和年龄 -->
					<tag-sex-age :sex="item.sex" :age="item.age"></tag-sex-age>
				</view>
				<view v-show="!isguanzhu" class="icon iconfont icon-zengjia" @tap="guanzhu">关注</view>
			</view>
			<!-- 第2行 -->
			<view>{{item.title}}</view>
			<!-- 第3行 -->
			<view class="u-f-ajc">
				<!-- 图片 -->
				<image v-if="item.titlepic" :src="item.titlepic" mode="widthFix" lazy-load></image>
				<!-- 视频 -->
				<template v-if="item.video">
					<view class="common-list-play icon iconfont icon-bofang"></view>
					<view class="common-list-playinfo">
						{{item.video.looknum}} 次播放 {{item.video.long}}
					</view>
				</template>
				<!-- 分享元素样式：左边-》图片，右边-》标题 -->
				<view class="common-list-share u-f-ac" v-if="item.share">
					<image :src="item.share.titlepic" mode="widthFix" lazy-load></image>
					<view>{{item.share.title}}</view>
				</view>
			</view>
			<!-- 第4行 -->
			<view class="u-f-ac u-f-jsb">
				<view>{{item.path}}</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa">{{item.sharenum}}</view>
					<view class="icon iconfont icon-pinglun1">{{item.commentnum}}</view>
					<view class="icon iconfont icon-dianzan1">{{item.goodnum}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import tagSexAge from "./tag-sex-age.vue";
	
	export default {
		components: {
			tagSexAge,
		},
		props: {
			item: {
				type: Object,
			},
			index: {
				type: Number,
			},
		},
		data() {
			return {
				isguanzhu: this.item.isguanzhu
			};
		},
		methods: {
			guanzhu() {
				this.isguanzhu = true;
				uni.showToast({
					title:"关注成功",
				});
			},
		},
	}
</script>

<style scoped>
	@import url("../../common/list.css");
</style>
