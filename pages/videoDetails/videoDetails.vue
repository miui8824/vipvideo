<template>
	<view>
		<video :src="play.url" id="myvideo" autoplay></video>
		<view class="btn-group">
			<view v-for="(item, i) in videoData" :key="i" class="u-button">
				<u-button hair-line plain ripple size="medium" @click="onChage(i)" :type="onchange === i ? 'primary' : 'warning'">{{ item.label }}</u-button>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			videoData: [
				{ label: '第23集', url: 'http://ik.hhshsq.cn:9200/23.mp4' },
				{ label: '第24集', url: 'http://ik.hhshsq.cn:9200/24.mp4' },
				{ label: '第25集', url: 'http://ik.hhshsq.cn:9200/25.mp4' },
				{ label: '第26集', url: 'http://ik.hhshsq.cn:9200/26.mp4' },
				{ label: '第27集', url: 'http://ik.hhshsq.cn:9200/27.mp4' },
				{ label: '第28集', url: 'http://ik.hhshsq.cn:9200/28.mp4' },
				{ label: '第29集', url: 'http://ik.hhshsq.cn:9200/28.mp4', value: 29 },
				{ label: '第30集', url: 'http://ik.hhshsq.cn:9200/28.mp4', value: 30 }
			],
			onchange: 0,
			play: {},
			videoContext: {}
		};
	},
	onLoad() {
		this.videoContext = uni.createVideoContext('myvideo', this);
		this.play = this.videoData[this.onchange];
		uni.setNavigationBarTitle({
			title: this.play.label
		});
	},
	onShareAppMessage() {
		return {
			title: '你微笑时很美',
			path: 'pages/index/index'
		};
	},
	methods: {
		onChage(e) {
			let that = this;
			console.log(e);
			const value = this.videoData[e];
			if (value.value == 29 || value.value == 30) {
				const info = wx.getSystemInfoSync();
				console.log(info);
				if (info.platform === 'android') {
					this.onchange = e;
					this.play = this.videoData[e];
					uni.setNavigationBarTitle({
						title: this.play.label
					});
					setTimeout(() => {
						this.videoContext.play();
					}, 200);
				} else {
					uni.showModal({
						title: '温馨提示:',
						content: '你是我的小宝贝吗？',
						confirmText: '是',
						cancelText: '不是',
						success(res) {
							if (res.confirm) {
								that.onchange = e;
								that.play = that.videoData[e];
								uni.setNavigationBarTitle({
									title: that.play.label
								});
								setTimeout(() => {
									that.videoContext.play();
								}, 200);
							} else {
								uni.showToast({
									title: '不是小宝贝不能看哦！嘻嘻',
									icon: 'none'
								});
							}
						},
						fail() {}
					});
				}

				return;
			}
			this.onchange = e;
			this.play = this.videoData[e];
			uni.setNavigationBarTitle({
				title: this.play.label
			});
			setTimeout(() => {
				this.videoContext.play();
			}, 200);
		}
	}
};
</script>

<style lang="less">
.content {
	box-sizing: border-box;
}
video {
	width: 100%;
	height: 375rpx;
}
.btn-group {
	display: flex;
	flex-wrap: wrap;
	align-items: center;
	// justify-content: flex-start;
	// justify-content: space-around;
	// padding: 0 24px;
	// margin-top: 24px;
}
.u-button {
	// width: 100rpx;
	// margin: 10rpx 20rpx;
	margin-left: 20rpx;
	margin-bottom: 16rpx;
	margin-top: 24rpx;
	.u-btn {
		// width: 200rpx;
	}
}
</style>
