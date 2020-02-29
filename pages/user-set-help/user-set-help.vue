<template>
	<view>
		<block v-for="(item, index) in list" :key="index">
			<uni-collapse>
				<uni-collapse-item :title="item.title" :showAnimation="true">
					<view style="padding: 30rpx;">{{item.content}}</view>
				</uni-collapse-item>
			</uni-collapse>
		</block>

		<view class="body">
			<button type="primary" class="user-set-btn">意见反馈</button>
		</view>
	</view>
</template>

<script>
	import uniCollapse from '@/components/uni-collapse/uni-collapse.vue'
	import uniCollapseItem from '@/components/uni-collapse-item/uni-collapse-item.vue'

	export default {
		components: {
			uniCollapse,
			uniCollapseItem,
		},
		data() {
			return {
				list: [{
						title: "客服什么时候上线？",
						content: "123"
					},
					{
						title: "忘记账号/昵称/密码怎么办？",
						content: "11111111"
					},
					{
						title: "怎么搜索/查找/关注/取关用户？",
						content: "222222222"
					}
				]
			}
		},
		methods: {

		}
	}
</script>

<style>
	/* css 引入需要放到第一行 */
	@import url("../../common/form.css");
</style>
