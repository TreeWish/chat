<template>
	<view>
		<!-- 聊天时间显示 -->
		<view v-if="showTime" class="flex align-center justify-center pb-4 pt-2">
			<text class="font-sm text-light-muted">{{showTime}}</text>
		</view>
		<!-- 聊天内容列表 -->
		<view class="flex px-2 align-start justify-start position-relative mb-3" :class="isSelf ? 'justify-end' : 'justify-start'">
			<template v-if="!isSelf">
				<avatar size="70" :src="item.avatar"></avatar>
				<text class="iconfont font-md position-absolute" style="left: 98rpx;top: 25rpx;color: #fff;">&#xebf6;</text>
			</template>
			<view :class="isSelf ? 'mr-3 bg-chat-item' : 'bg-white ml-3'" class="py-2 px-1 rounded " style="max-width: 500rpx;padding-left: 15rpx;">
				<text @longpress="longClick" class="font-md">{{ item.data }}</text>
			</view>
			<template v-if="isSelf">
				<text class="iconfont font-md position-absolute text-chat-item" style="right: 98rpx;top: 25rpx;">&#xe62d;</text>
				<avatar size="70" :src="item.avatar"></avatar>
			</template>
		</view>
	</view>
</template>

<script>
	import $Time from '@/common/free-lib/time.js'
	import popup from '@/components/popup/popup.vue'
export default {
	mixins: ['$Time'],
	props: {
		item: {
			type: Object,
			default: {}
		},
		pretime: {
			type: Number,
			default: 0
		}
	},
	data() {
		return {
			
		};
	},
	onLoad() {
		// #ifdef APP-PLUS-NVUE
		// 加载公共图标库
		const domModule = weex.requireModule('dom');
		domModule.addRule('fontFace', {
			fontFamily: 'iconfont',
			src: "url('https://at.alicdn.com/t/font_2142552_awkanprjly9.ttf')"
		});
		// #endif
	},
	methods: {
		longClick(e, index) {
			let x = 0;
			let y = 0;
			// #ifdef APP-PLUS-NVUE
			if (Array.isArray(e.touches) && e.touches.length > 0) {
				x = e.touches[0].screenX;
				y = e.touches[0].screenY;
			}
			// #endif
			// #ifdef MP-WEIXIN
			if (Array.isArray(e.touches) && e.touches.length > 0) {
				x = e.detail.x;
				y = e.detail.y;
			}
			// #endif
			this.$emit('long', { x, y, index });
		}
	},
	computed: {
		isSelf() {
			let self = 1;
			return this.item.user_id === 1;
		},
		showTime() {
			return $Time.getChatTime(this.item.create_time, this.pretime)
		}
	}
};
</script>

<style></style>
