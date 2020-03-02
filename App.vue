<script>
	export default {
		onLaunch: function() {
			// console.log('--- 演示调用 config.js 中的 webUrl ---' + this.config.webUrl)
			// this.lib.ceshi();
			
			// 对网络进行监听(用户目前断网,切换wifi)
			this.lib.NetWork.On();
			
			// 更新检测
			
			
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	/* uni.css - 通用组件、模板样式库，可以当作一套ui库应用 */
	
	/* 引入官方css库 */
	@import './common/uni.css';
	
	/* 引入自定义图标库 */
	@import './common/icon.css';
	/* 引入自定义动画库 */
	@import './common/animate.css';
	
	/* 自定义公共样式 */
	@import './common/common.css';
	
</style>
