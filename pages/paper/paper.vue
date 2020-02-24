<template>
	<view class="body">
		<!-- 小纸条列表 -->
		<block v-for="(item, index) in list" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>
	</view>
</template>

<script>
	import paperList from '../../components/paper/paper-list.vue';

	export default {
		components: {
			paperList,
		},
		data() {
			return {
				list:[
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称1",
						time:"10:21",
						data:"我是信息1",
						noreadnum:2,
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称2",
						time:"10:21",
						data:"我是信息2",
						noreadnum:0,
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称3",
						time:"10:21",
						data:"我是信息3",
						noreadnum:0,
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称4",
						time:"10:21",
						data:"我是信息4",
						noreadnum:11,
					},
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
</style>
