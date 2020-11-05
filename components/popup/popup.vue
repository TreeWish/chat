<template>
	<view style="z-index: 999;overflow: hidden;" v-if="isShow">
		<!-- 蒙版 -->
		<view v-if="mask" class="position-fixed top-0 left-0 right-0 bottom-0" :style="getMaskColor" @click="hide"></view>
		<!-- 弹出框内容 -->
		<view :class="popupClass" class="position-fixed bg-white" :style="popupPostion"><view style="height: 300rpx;">123</view></view>
	</view>
</template>

<script>
export default {
	props: {
		isShow: {
			type: Boolean,
			default: false
		},
		maskColor: {
			type: Boolean,
			default: false
		},
		mask: {
			type: Boolean,
			default: false
		},
		postion: {
			type: String,
			default: ''
		}
	},
	data() {
		return {};
	},
	computed: {
		getMaskColor() {
			let color = this.maskColor ? 0.5 : 0;
			return `background-color: rgba(0,0,0,${color})`;
		},
		// 获取弹出层位置
		popupPostion() {
			let postion = this.postion ? this.postion : 'left: 0;right:0;bottom:0';
			return postion;
		},
		popupClass() {
			if(this.postion.length) {
				return 'rounded border'
			}
		}
	},
	methods: {
		show() {
			this.isShow = true;
		},
		hide() {
			this.isShow = false;
			console.log('hide');
		}
	},
	mounted() {
		console.log(this.popupPostion);
	}
};
</script>

<style></style>
