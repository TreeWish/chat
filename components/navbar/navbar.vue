<template>
	<view>
		<!-- 导航条 -->
		<view :class="bgClass">
			<!-- 状态栏 -->
			<view :style="'height:' + statusBarHeight + 'px'"></view>
			<!-- 导航 -->
			<view class="w-100 flex justify-between align-center" style="height: 90rpx;">
				<view class="flex align-center">
					<iconbtn v-if="showBack" :icon="'\uebf5'" @click="back"></iconbtn>
					<text v-if="title" class="font-md ml-3">{{ getTitle }}</text>
				</view>
				<view class="flex align-center">
					<slot name="iconbtn">
						<iconbtn :icon="'\ue650'"></iconbtn>
						<iconbtn :icon="'\ue664'" @click="openExtend"></iconbtn>
					</slot>
				</view>
			</view>
		</view>
		<view v-if="fixed" :style="fixedStyle"></view>
		<popup width="105" height="320" ref="openExtend">
			<view style="width: 320rpx;height: 525rpx;" :style="menuStyle" class="flex flex-column">
				<view class="flex-1 flex align-center bg-dark" hover-class="bg-hover-dark" v-for="item in 5">
					<text class="iconfont font-md text-white pl-3 pr-2">&#xe650;</text>
					<text class="font-md text-white">标记以读</text>
				</view>
			</view>
		</popup>
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
		},
		bgColor: {
			type: String,
			default: 'bg-light'
		},
		showBack: {
			type: Boolean,
			default: false
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
			let title = this.title;
			if (title === '微信') {
				title = this.noreadNum > 0 ? `${this.title}(${this.noreadNum})` : this.title;
			}
			return title;
		},
		bgClass() {
			let bg = this.bgColor ? this.bgColor : 'bg-light';
			return `${bg} fixed-top`;
		}
	},
	methods: {
		openExtend() {
			console.log('open');
			this.$refs.openExtend.show(uni.upx2px(415), uni.upx2px(150));
			// this.$emit('openExtend')
		},
		back() {
			uni.navigateBack();
		}
	}
};
</script>

<style></style>
