<template>
	<view>
		<!-- 导航条 -->
		<view class="bg-light fixed-top">
			<!-- 状态栏 -->
			<view :style="'height:' + statusBarHeight + 'px'"></view>
			<!-- 导航 -->
			<view class="w-100 flex justify-between align-center" style="height: 90rpx;">
				<view class="flex align-center"><text v-if="title" class="font-md ml-3">{{getTitle}}</text></view>
				<view class="flex align-center">
					<iconbtn :icon="'\ue650'"></iconbtn>
					<iconbtn :icon="'\ue664'" @click="openExtend"></iconbtn>
				</view>
			</view>
		</view>
		<view v-if="fixed" :style="fixedStyle"></view>
	</view>
</template>

<script>
import iconbtn from '@/components/iconbtn/iconbtn';
export default {
	components: {
		iconbtn
	},
	props: {
		fixed: {
			type: Boolean,
			default: true
		},
		title: {
			type: String,
			default: ''
		}
	},
	data() {
		return {
			statusBarHeight: 0,
			navBarHeight: 0,
			isShow: false,
			noreadNum: 1
		};
	},
	mounted() {
		console.log(this.title);
		// #ifdef APP-PLUS-NVUE
		this.statusBarHeight = plus.navigator.getStatusbarHeight();
		// #endif
		this.navBarHeight = this.statusBarHeight + uni.upx2px(90);
	},
	computed: {
		fixedStyle() {
			return `height: ${this.navBarHeight}px`;
		},
		getTitle() {
			let title = this.noreadNum >0 ? `${this.title}(${this.noreadNum})`: this.title
			return title
		}
	},
	methods: {
		openExtend() {
			console.log('open');
			this.$emit('openExtend')
		}
	},
};
</script>

<style></style>
