<script>
export default {
	onLaunch: function() {
		// #ifdef APP-PLUS-NVUE
		// 加载公共图标库
		const domModule = weex.requireModule('dom');
		domModule.addRule('fontFace', {
			fontFamily: 'iconfont',
			src: "url('https://at.alicdn.com/t/font_2142552_b0ffpxc0s8.ttf')"
		});
		// #endif
		console.log('App Launch');
	},
	onShow: function() {
		console.log('App Show');
	},
	onHide: function() {
		console.log('App Hide');
	}
};
</script>

<style>
/*每个页面公共css */
@import './common/free.css';
@import './common/common.css';
/* #ifndef APP-PLUS-NVUE */
@import './common/icon.css';
/* #endif */

/* #ifdef MP */
::-webkit-scrollbar {
	display: none;
}
/* #endif */
</style>
