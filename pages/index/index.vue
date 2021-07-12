<template>
	<view class="content">
		<view class="videocard" @click="natodetails">
			<view class="image_card">
				<image src="//puui.qpic.cn/vcover_vt_pic/0/mzc0020073xzbad1624242335951/350" mode="aspectFill"></image>
				<view class="update_timer">更新至28级</view>
			</view>
			<view class="videoName">你微笑时很美</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			title: 'Hello'
		};
	},
	onLoad() {},
	methods: {
		natodetails() {
			uni.navigateTo({
				url: '../videoDetails/videoDetails'
			});
		}
	}
};
</script>

<style lang="less">
.content {
	padding: 24rpx;
	box-sizing: border-box;
	font-size: 24rpx;
}
.videocard {
	border-radius: 8rpx;
	overflow: hidden;
	.image_card {
		width: 180rpx;
		height: 250rpx;
		position: relative;
	}
	.update_timer {
		position: absolute;
		bottom: 12rpx;
		right: 12rpx;
		color: #fff;
		font-size: 24rpx;
	}
	image {
		width: 100%;
		height: 100%;
		display: block;
	}
}
</style>
