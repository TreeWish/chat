<template>
	<view class="flex align-stretch" hover-class="bg-hover-light">
		<!--  @click="chatClick" @longpress="longClick" -->
		<view class="flex align-center justify-center position-relative" style="width: 145rpx;">
			<avatar src="/static/images/mail/tag.png"></avatar>
			<badge :value="4" class="position-absolute" style="right: 15rpx;top: 15rpx;"></badge>
		</view>
		<view class="flex flex-column flex-1 py-3 pr-3 border-bottom border-light-secondary">
			<view class="flex align-center justify-between mb-1">
				<text class="font-md">昵称</text>
				<text class="font-sm text-light-muted">{{1603422809 | dateFomate}}</text>
			</view>
			<text class="font text-ellipsis text-light-muted">消息内容</text>
		</view>
	</view>
</template>

<script>
import $Time from '@/common/free-lib/time.js';
export default {
	data() {
		return {};
	},
	filters: {
		dateFomate(value) {
			return $Time.gettime(value);
		}
	},
	methods: {
		chatClick() {
			console.log('click');
		},
		longClick(e) {
			console.log(e);
		}
	}
};
</script>

<style></style>
