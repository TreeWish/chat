<template>
	<view>
		<view
			class="flex justify-center align-center"
			style="width: 90rpx;height: 90rpx;"
			hover-class="bg-hover-light" @click="$emit('click')">
			<text class="iconfont font-md">{{icon}}</text>
		</view>
	</view>
</template>

<script>
export default {
	props: {
		icon: {
			type: String,
			default: ''
		}
	},
	data() {
		return {};
	}
};
</script>

<style></style>
