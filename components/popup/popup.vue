<template>
	<view style="z-index: 999;overflow: hidden;" v-if="isShow">
		<!-- 蒙版 -->
		<view 
		v-if="mask"
		class="position-fixed top-0 left-0 right-0 bottom-0"
		:style="getMaskColor"
		@click="hide"></view>
		<!-- 弹出框内容 -->
		<view class="position-fixed bg-white" :style="getMaskPostion">
			<view style="height: 300rpx;"></view>
		</view>
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
		getMaskPostion() {
			let postion = this.postion ? this.postion : 'left: 0;right:0;bottom:0';
			return postion;
		}
	},
	methods: {
		hide() {
			this.isShow = false;
			console.log('hide');
		}
	},
	mounted() {
		console.log(this.getMaskPostion);
	}
};
</script>

<style></style>
