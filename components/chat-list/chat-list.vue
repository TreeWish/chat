<template>
	<view :class="item.isTop ? 'bg-light' : 'bg-white'" class="flex align-stretch" hover-class="bg-hover-light" @longpress="longClick($event, index)" @click="chatClick(index)">
		<view class="flex align-center justify-center position-relative" style="width: 145rpx;">
			<avatar src="/static/images/mail/tag.png"></avatar>
			<badge :value="item.noReadNum" class="position-absolute" style="right: 15rpx;top: 15rpx;"></badge>
		</view>
		<view class="flex flex-column flex-1 py-3 pr-3 border-bottom border-light-secondary">
			<view class="flex align-center justify-between mb-1">
				<text class="font-md">{{ item.nickname }}</text>
				<text class="font-sm text-light-muted">{{ item.time | dateFomate }}</text>
			</view>
			<text class="font text-ellipsis text-light-muted">{{ item.content }}</text>
		</view>
	</view>
</template>

<script>
import $Time from '@/common/free-lib/time.js';
export default {
	props: {
		item: {
			type: Array,
			default: []
		},
		index: {
			type: Number,
			default: 0
		}
	},
	data() {
		return {
			chatList: [
				{
					nickname: '昵称',
					noReadNum: 4,
					time: 1603422809,
					content: '消息内容'
				},
				{
					nickname: '昵称2',
					noReadNum: 2,
					time: 1603422809,
					content: '消息内容'
				},
				{
					nickname: '昵称3',
					noReadNum: 3,
					time: 1603422809,
					content: '消息内容'
				},
				{
					nickname: '昵称4',
					noReadNum: 1,
					time: 1603422809,
					content: '消息内容'
				}
			]
		};
	},
	filters: {
		dateFomate(value) {
			return $Time.gettime(value);
		}
	},
	methods: {
		chatClick(event) {
			console.log(event);
		},

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
	}
};
</script>

<style></style>
