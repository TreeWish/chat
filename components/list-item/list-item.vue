<template>
	<view class="flex align-stretch bg-white">
		<view class="flex align-center justify-center px-3 py-2">
			<slot name="icon"></slot>
			<image v-if="showAvatar" src="/static/images/mail/friend.png" :style="avatarSize" mode="widthFix"></image>
		</view>
		<view class="flex-1 border-bottom flex align-center flex justify-between pr-3">
			<slot><text class="font-md text-dark">{{title}}</text></slot>
			<view class="flex align-center">
				<slot name="avatar"></slot>
				<text v-if="showRight" class="iconfont font-md text-light-muted">&#xe665;</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props: {
			showRight: {
				type: Boolean,
				default: false
			},
			title: {
				type: String,
				default: ''
			},
			imgSize: {
				type: [String, Number],
				default: 75
			}
		},
		data() {
			return {
				
			};
		},
		computed: {
			avatarSize() {
				// 报错
				return `width: ${this.imgSize}rpx;height: ${this.imgSize}rpx;` 
			},
			showAvatar() {
				if(this.showRight && this.imgSize == 75) {
					return false
				} else {
					return true
				}
			}
		},
	}
</script>

<style>

</style>
