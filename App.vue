<script>
	import Vue from 'vue'
	
	export default {
		onLaunch: function() {
			console.log('App Launch');
			uni.getSystemInfo({
				success: function(e) {
					// 自定义导航栏高度计算
					// #ifndef MP
					Vue.prototype.StatusBar = e.statusBarHeight;
					if (e.platform == 'android') {
						Vue.prototype.CustomBar = e.statusBarHeight + 50;
					} else {
						Vue.prototype.CustomBar = e.statusBarHeight + 45;
					};
					// #endif
					// #ifdef MP-WEIXIN
					Vue.prototype.StatusBar = e.statusBarHeight;
					let custom = wx.getMenuButtonBoundingClientRect();
					Vue.prototype.Custom = custom;
					Vue.prototype.CustomBar = custom.bottom + custom.top - e.statusBarHeight;
					// #endif       
					// #ifdef MP-ALIPAY
					Vue.prototype.StatusBar = e.statusBarHeight;
					Vue.prototype.CustomBar = e.statusBarHeight + e.titleBarHeight;
					// #endif
					
					// 可用窗口宽度
					// #ifdef MP-WEIXIN
					Vue.prototype.AvailableHeight = e.windowHeight + e.statusBarHeight;
					// #endif
					// #ifdef H5
					Vue.prototype.AvailableHeight = e.windowHeight - e.statusBarHeight;
					// #endif
				}
			})
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
@import "components/colorui/main.css";
@import "components/colorui/icon.css";
</style>
