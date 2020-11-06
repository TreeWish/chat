<template>
	<view style="z-index: 999;overflow: hidden;" v-if="isShow">
		<!-- 蒙版 -->
		<view v-if="mask" class="position-fixed top-0 left-0 right-0 bottom-0" :style="getMaskColor" @click="hide"></view>
		<!-- 弹出框内容 -->
		<view :class="popupClass" class="position-fixed bg-white" :style="popupPostion">
			<view :style="menuStyle" class="flex flex-column">
				<text class="font-md flex-1 flex align-center p-3" hover-class="bg-hover-light">标记以读</text>
				<text class="font-md flex-1 flex align-center p-3" hover-class="bg-hover-light">置顶聊天</text>
				<text class="font-md flex-1 flex align-center p-3" hover-class="bg-hover-light">删除该聊天</text>
			</view>
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
			let left = this.x >-1 ?`left:${this.x}px;` : '';
			let top = this.y >-1 ?`top:${this.y}px;` : '';
			let postion = this.postion ? `${left+top}` : 'left: 0;right:0;bottom:0';
			return postion;
		},
		popupClass() {
			let postion = this.postion ? 'left-0;right-0;bottom-0' :'rounded border';
			return postion
		},
		menuStyle() {
			let height = 100;
			const width = 240; 
			height = height * this.menu
			return `width: ${width}rpx;height:${height}rpx`
		}
	},
	methods: {
		show(x, y) {
			if(x && y) {
				this.postion = true
				this.x = x > this.maxX ? this.maxX : x;
				this.y = y > this.maxY ? this.maxY : y;
			} else {
				this.postion = false
			}
			console.log(this.popupPostion);
			this.isShow = true;
		},
		hide() {
			this.isShow = false;
			console.log('hide');
		}
	},
	mounted() {

		try{
			const info = uni.getSystemInfoSync()
			this.maxX = info.windowWidth - uni.upx2px(this.width)
			this.maxY = info.windowHeight - uni.upx2px(this.height)
		}catch(e){
			//TODO handle the exception
			
		}
	}
};
</script>

<style></style>
