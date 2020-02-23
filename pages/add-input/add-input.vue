<template>
	<view>

		<!-- 发布页：自定义导航栏 -->
		<uni-nav-bar left-icon="arrowleft" @clickLeft="back" @clickRight="submit" :statusBar="true" rightText="发布">
			<view class="u-f-ajc" style="margin:auto;" @tap="changelook">
				{{yinsi}}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>

		<!-- 多行输入框 -->
		<view class="uni-textarea">
			<textarea placeholder="说一句话吧~" v-model="text"></textarea>
		</view>

		<!-- 上传多图 -->
		<upload-images @upload="upload"></upload-images>

		<!-- 弹出公告 -->
		<uni-popup :show="showpopup" position="middle" mode="fixed" @change="hidePopup">
			<view class="gonggao">
				<view class="u-f-ajc">
					<image src="../../static/common/addinput.png" mode="widthFix"></image>
				</view>
				<view>1. 涉及黄色，政治，广告及骚扰信息。</view>
				<view>2. 涉及黄色，政治，广告及骚扰信息。</view>
				<view>3. 涉及黄色，政治，广告及骚扰信息。</view>
				<view>4. 涉及黄色，政治，广告及骚扰信息。</view>
				<button type="default" @tap="hidePopup">朕知道了</button>
			</view>
		</uni-popup>

	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue";
	import uploadImages from "../../components/common/upload-images.vue"
	import uniPopup from "../../components/uni-popup/uni-popup.vue"

	let changelook = ['所有人可见', '仅自己可见'];

	export default {
		components: {
			uniNavBar,
			uploadImages,
			uniPopup,
		},
		data() {
			return {
				yinsi: "所有人可见",
				text: "",
				imgList: [], // 从子组件传入
				showpopup: false,
				isget: false,
			}
		},
		methods: {
			//返回事件
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			// 发布事件
			submit() {
				console.log("发布事件")
			},
			// 隐私
			changelook() {
				uni.showActionSheet({
					itemList: changelook,
					success: (res) => {
						this.yinsi = changelook[res.tapIndex]
					},
				});
			},
			// 多图上传 - 监听子组件，在提交和删除的时候，从子组件传入imageList
			upload: function(arr) {
				this.imgList = arr;
				console.log("ImageList: " + this.imgList)
			},
			// 隐藏Popup
			hidePopup(e) {
				if (!e.show) {
					console.log("隐藏popup");
					this.showpopup = false;
				}
			},
			// 保存为草稿
			baocun() {
				uni.showModal({
					content: "是否要保存为草稿？",
					cancelText: "不保存",
					confirmText: "保存",
					success: (res) => {
						if (res.confirm) {
							// TODO: 后面对接接口的时候再进行编写
							console.log("保存");
						} else {
							// TODO: 后面对接接口的时候再进行编写
							console.log("不保存");
						}
						this.isget = true;
						uni.navigateBack({
							delta: 1,
						});
					}
				});
			},
		},
		// 监听页面初次渲染完成。注意如果渲染速度快，会在页面进入动画完成前触发
		onReady() {
			this.showpopup = true;
		},
		// 监听用户返回事件
		onBackPress() {
			console.log("监听用户返回事件");
			// 判断用户是否已经更改了信息
			// 没有进行任何更改，不需要保存为草稿
			if (!this.text && this.imgList.length == 0) {
				return;
			}
			// 已经进行更改了
			if (!this.isget) {
				this.baocun();
				// true 表示不返回
				return true;
			}
		}
	}
</script>

<style>
	.uni-textarea {
		border: 1rpx solid #EEE;
	}

	.gonggao {
		width: 500rpx;
		background-color: white;
		padding: 40rpx;
		border-radius: 20rpx;
	}

	.gonggao image {
		width: 75%;
		margin-bottom: 20rpx;
	}

	.gonggao button {
		background: #FFE934;
		color: #171606;
		margin-top: 20rpx;
	}
</style>
