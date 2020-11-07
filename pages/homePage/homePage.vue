<template>
	<view>
		<view class="cu-bar bg-white solid-bottom">
			<view class="action">
				<text class="cuIcon-title text-ryr"></text>正在读
			</view>
			<view class="action">
				<text class="cuIcon-roundadd"></text>
				<text class="text-df">添加书本</text>
			</view>
		</view>
		<view class="padding-xs">
			<view class="cu-list margin-top">
				<view class="cu-item bg-white radius" v-for="(item, index) in readingList" :key="index">
					<view class="flex margin-bottom margin-lr-xs align-center">
						<view class="flex-sub text-left padding">
							<view class="cu-avatar book" :style="[{backgroundImage:'url('+ item.images_medium +')'}]"></view>
						</view>
						<view class="flex-twice padding">
							<view class="text-bold">{{item.title}}</view>
							<view class="text-gray text-sm margin-top-xs">
								<text class="cuIcon-myfill margin-right-xs"></text>
								{{item.author}}
							</view>
							<view class="text-gray text-sm margin-top-xs">
								<text class="cuIcon-newsfill margin-right-xs"></text>
								{{item.pubdate}}
							</view>
							<view class="text-gray text-sm margin-top-xs">
								<text class="cuIcon-timefill margin-right-xs"></text>
								{{item.publisher}}
							</view>
						</view>
						<view class="flex-sub align-center">
							<canvas v-if="!(item.img)" :canvas-id="'canvasGauge' + index" class="charts"/>
							<image v-else :src="item.img" class="charts"></image>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uCharts from '../../components/u-charts/u-charts.js';
	var _self;
	var canvasGauge = null;
	
	export default {
		data() {
			return {
				rWidth: '',
				rHeight: '',
				pixelRatio:1,
				categories: [{
								value: 0.2,
								color: '#7BD0CD'
							}, {
								value: 0.8,
								color: '#5CD0CC'
							}, {
								value: 1,
								color: '#29A19C'
							}],
							series: [{
								name: '当前进度',
								data: 0.85
							}],
				readingList: [
					{
						"levelNum":"8.0",
						 "subtitle":"",
						 "author":" 加西亚·马尔克斯",
						 "pubdate":"2012-9-1",
						 "origin_title": "El amor en los tiempos del cólera",
						 "binding":"精装",
						 "pages":"401",
						 "images_medium":"http://open.6api.net/mpic/s11284102.jpg",
						 "images_large":"http://open.6api.net/lpic/s11284102.jpg",
						 "publisher":"南海出版公司",
						 "isbn10":"7544258971",
						 "isbn13":"9787544258975",
						 "title":"霍乱时期的爱情",
						 "summary":"霍乱时期的爱情》是加西亚•马尔克斯获得诺贝尔文学奖之后完成的第一部小说。讲述了一段跨越半个多世纪的爱情史诗，穷尽了所有爱情的可能性：忠贞的、隐秘的、粗暴的、羞怯的、柏拉图式的、放荡的、转瞬即逝的、生死相依的……再现了时光的无情流逝，被誉为“人类有史以来最伟大的爱情小说”，是20世纪最重要的经典文学巨著之一。",
						 "price":"39.50元",
						 process: {data: 0.7}
					},
					{
						"levelNum":"8.0",
						 "subtitle":"",
						 "author":" 加西亚·马尔克斯",
						 "pubdate":"2012-9-1",
						 "origin_title": "El amor en los tiempos del cólera",
						 "binding":"精装",
						 "pages":"401",
						 "images_medium":"http://open.6api.net/mpic/s11284102.jpg",
						 "images_large":"http://open.6api.net/lpic/s11284102.jpg",
						 "publisher":"南海出版公司",
						 "isbn10":"7544258971",
						 "isbn13":"9787544258975",
						 "title":"霍乱时期的爱情",
						 "summary":"霍乱时期的爱情》是加西亚•马尔克斯获得诺贝尔文学奖之后完成的第一部小说。讲述了一段跨越半个多世纪的爱情史诗，穷尽了所有爱情的可能性：忠贞的、隐秘的、粗暴的、羞怯的、柏拉图式的、放荡的、转瞬即逝的、生死相依的……再现了时光的无情流逝，被誉为“人类有史以来最伟大的爱情小说”，是20世纪最重要的经典文学巨著之一。",
						 "price":"39.50元",
						 process: {data: 0}
					}
				]
			}
		},
		methods: {
			// 初始化仪表盘
			initCharts() {
				let _this = this;
				if(this.readingList.length > 0) {
					this.readingList.forEach((item, index) => {
						_this.showGauge('canvasGauge' + index, item, index);
					});
				}
			},
			showGauge(canvasId, chartData, index) {
				canvasGauge = new uCharts({
					$this: _self,
					canvasId: canvasId,
					type: 'gauge',
					legend:false,
					title: {
						name: Math.round(chartData.process.data*100)+'%',
						color: '#29A19C',
						fontSize: 20,
						offsetY: 45,
					},
					subtitle: {
						name: '当前进度',
						color: '#666666',
						fontSize: 10,
						offsetY: 10,
					},
					extra: {
						gauge:{
							type:'default',
							width:10,//仪表盘背景的宽度
							startAngle:0.75,
							endAngle:0.25,
							startNumber:0,
							endNumber:100,
							splitLine:{
								fixRadius:0,
								splitNumber:10,
								width: 10,//仪表盘背景的宽度
								color:'#FFFFFF',
								childNumber:5,
								childWidth:4,//仪表盘背景的宽度
							},
							pointer:{
								width: 8,//指针宽度
								color:'auto'
							}
						}
					},
					background:'#FFFFFF',
					pixelRatio:1,
					categories: _self.categories,
					series: [chartData.process],
					animation: true,
					width: this.rWidth,
					height: this.rHeight,
					disablePieStroke: true,
					dataLabel: false,
				});
				
				// 渲染完成将canvas转成图片
				canvasGauge.addEventListener('renderComplete', () => {//监控图表渲染完成
					setTimeout(function(){//延迟一定时间执行
						uni.canvasToTempFilePath({//将图表转成图片
							x: 0,
							y: 0,
							width: _self.rWidth * _self.pixelRatio,
							height: _self.rHeight * _self.pixelRatio,
							fileType:'png',
							canvasId: canvasId,
							success: function(res) {
								_self.readingList[index].img=res.tempFilePath;
							},
							fail:function(res){
							}
						},_self);
					},100);
				});
			}
		},
		onShow() {
			// 初始化环状图
			_self = this;
			this.rWidth = uni.upx2px(200);
			this.rHeight = uni.upx2px(200);
			this.initCharts();
		}
	}
</script>

<style>
.charts {
	width: 200upx;
	height: 200upx;
	background-color: #FFFFFF;
}
</style>
