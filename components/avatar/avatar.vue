<template>
	<view>
		<image :src="src" mode="widthFix" :style="getSize" class="rounded"></image>
	</view>
</template>

<script>
	export default {
		props: {
			src: {
				type: String,
				default: ''
			},
			size: {
				type: [String, Number],
				default: 92
			}
		},
		data() {
			return {
				
			};
		},
		computed: {
			getSize() {
				return `width: ${this.size}rpx;height: ${this.size}rpx;`
			}
		},
	}
</script>

<style>

</style>
