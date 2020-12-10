<template>
	<view style="z-index: 999;overflow: hidden;" v-if="isShow">
		<!-- 蒙版 -->
		<view v-if="mask" class="position-fixed top-0 left-0 right-0 bottom-0" :style="getMaskColor" @click="hide"></view>
		<!-- 弹出框内容 -->
		<view :class="popupClass" class="position-fixed bg-white animate" :style="popupPostion" ref="pop"><slot></slot></view>
	</view>
</template>

<script>
const animation = weex.requireModule('animation');
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
			default: true
		},
		// 是否处于底部
		postion: {
			type: Boolean,
			default: false
		},
		width: {
			type: Number,
			default: 200
		},
		height: {
			type: Number,
			default: 100
		},
		tabBarHeight: {
			type: Number,
			default: 105
		}
	},
	data() {
		return {
			x: 0,
			y: 0,
			maxX: 0,
			maxY: 0,
			menu: 3
		};
	},
	computed: {
		getMaskColor() {
			let color = this.maskColor ? 0.5 : 0;
			return `background-color: rgba(0,0,0,${color})`;
		},
		// 获取弹出层位置
		popupPostion() {
			let left = this.x > -1 ? `left:${this.x}px;` : '';
			let top = this.y > -1 ? `top:${this.y}px;` : '';
			let postion = this.postion ? `${left + top}` : 'left: 0;right:0;bottom:0';
			return postion;
		},
		popupClass() {
			let postion = this.postion ? 'left-0;right-0;bottom-0' : 'rounded border';
			return postion;
		},
		menuStyle() {
			let height = 100;
			const width = 240;
			height = height * this.menu;
			return `width: ${width}rpx;height:${height}rpx`;
		}
	},
	methods: {
		show(x, y) {
			if (x && y) {
				this.postion = true;
				this.x = x > this.maxX ? this.maxX : x;
				this.y = y > this.maxY ? this.maxY : y;
			} else {
				this.postion = false;
			}
			this.isShow = true;
			// #ifdef APP-PLUS-NVUE
			this.$nextTick(() => {
				animation.transition(
					this.$refs.pop,
					{
						styles: {
							transform: 'scale(1, 1)',
							transformOrigin: 'left top',
							opacity: 1
						},
						duration: 100 //ms
					},
					() => {
						console.log('动画执行结束');
					}
				);
			});
			// #endif
		},
		hide() {
			// #ifdef APP-PLUS-NVUE
			let transformOrigin = 'left top'
			if(this.x == 415) {
				transformOrigin = 'right top'
			}
			animation.transition(
				this.$refs.pop,
				{
					styles: {
						transform: 'scale(0, 0)',
						opacity: 0,
						transformOrigin: transformOrigin
					},
					duration: 100
				},
				() => {
					this.isShow = false;
				}
			);
			// #endif
			// #ifndef APP-PLUS
			this.isShow = false;
			// #endif
			console.log('hide');
		}
	},
	mounted() {
		try {
			const info = uni.getSystemInfoSync();
			this.maxX = info.windowWidth - uni.upx2px(this.width);
			this.maxY = info.windowHeight - uni.upx2px(this.height) - uni.upx2px(this.tabBarHeight);
			console.log(this.height);
		} catch (e) {
			//TODO handle the exception
		}
	}
};
</script>

<style scoped>
.animate {
	/* #ifdef APP-PLUS-NVUE */
	transform: scale(0, 0);
	opacity: 0;

	/* #endif */
}
</style>
