<template>
	<view>
		<!-- 聊天页面底部输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
		
	</view>
</template>

<script>
	import userChatBottom from "../../components/user-chat/user-chat-bottom.vue"
	
	export default {
		components: {
			userChatBottom
		},
		data() {
			return {
				
			}
		},
		methods: {
			// 发送留言逻辑
			submit(data) {
				console.log("当前输入的是：" + data);
			}
		}
	}
</script>

<style>
	
</style>
