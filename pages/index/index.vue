<template>
	<view class="bg-img"
	:style="'height:' + bgHeight +'px;background-image: url('+ bgSrc +');'">
		<view class="text-center text-xxl" style="padding-top: 100%;">
			<view class="">
				<text class="text-bold text-white">{{title}}</text>
			</view>
			<view class="text-df padding-top text-right padding-right">
				<text class="text-white">{{subTitle}}</text>
			</view>
		</view>
		<view class="text-center" style="padding-top: 20%;">
			<navigator open-type="switchTab" url="../homePage/homePage">
				<button class="cu-btn round bg-ryr lg">
					开始体验
				</button>
			</navigator>
		</view>
	</view>
</template>

<script>
	import bgImg from '../../static/bg.jpg';
	export default {
		data() {
			return {
				bgHeight: this.AvailableHeight - 44,
				title: '阅读理当成为一种享受',
				subTitle: '—毛姆《毛姆读书随笔》',
				bgSrc: bgImg
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style>
	.content {
	}
</style>
