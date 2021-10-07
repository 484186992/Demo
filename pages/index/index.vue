<template>
	<view class="content">
		<image class="banner-img" src="https://www.zhaoxiedu.net/static/imgs/banner/%E4%B8%AA%E4%BA%BA%E4%B8%AD%E5%BF%83.jpg" mode="" />
		<view class="tip-box" v-if="!token">
			<text>您尚未登录，点我</text>
			<text class="color-btn" @click="goLogin">登录</text>
		</view>

		<view v-else class="tip-box">
			<text class="color-btn">Tina</text>
			<text>，欢迎你~</text>
		</view>

		<uni-title title1="VIP" title2="资源下载" text1="VIP学员可获取对应课程的视频源码" />

		<view class="course-box">
			<view @click="goCourse" v-for="i in resourceListByTypeVip" class="public-list">
				<image :src="baseUrl + i.imageUrl" mode="" />
				<text>{{ i.name }}</text>
			</view>
		</view>

		<uni-title title1="配套" title2="资源下载" text1="VIP学员可获取对应的配套学习资料" />

		<view class="course-box">
			<view v-for="i in resourceListByTypeSupporting" class="public-list">
				<image :src="baseUrl + i.imageUrl" mode="" />
				<text>{{ i.name }}</text>
			</view>
		</view>

		<uni-title title1="视频课" title2="资源下载" text1="独立的小额视频课资源" />

		<view class="course-box">
			<view v-for="i in resourceListByGift" class="public-list">
				<image :src="baseUrl + i.imageUrl" mode="" />
				<text>{{ i.name }}</text>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			resourceList: [],
			resourceListByTypeVip: [],
			resourceListByTypeSupporting: [],
			resourceListByGift: [],
			baseUrl: 'https://www.zhaoxiedu.net',
			token: ''
		};
	},
	onLoad() {
		let _this = this;
		uni.getStorage({
			key: 'token',
			success: function(res) {
				_this.token = res.data;
				console.log(_this.token);
			}
		});
		uni.request({
			url: 'https://www.fastmock.site/mock/b5b84dc2a6df42eb062ed5ee7bd72b4a/uni/getResourceList',
			success: res => {
				this.resourceList = res.data.data;
				(this.resourceListByTypeVip = this.resourceList.filter(m => m.type == 1)),
					(this.resourceListByTypeSupporting = this.resourceList.filter(m => m.type == 2)),
					(this.resourceListByGift = this.resourceList.filter(m => m.type == 3));
			}
		});
	},
	methods: {
		goCourse() {
			let _this = this;
			uni.getStorage({
				key: 'token',
				success: function(res) {
					console.log(res.data);
				},
				fail: function() {
					uni.showModal({
						title: '提示',
						content: 'VIP资源需要登录查看',
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确认');
								// 进入登录页面
								_this.goLogin();
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					});
				}
			});
		},
		goLogin() {
			uni.navigateTo({
				url: `/pages/login/login`
			});
		}
	}
};
</script>

<style scoped>
.course-box {
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	justify-content: space-between;
	padding: 10px;
}
.banner-img {
	width: 100%;
	height: 120px;
}
.public-list {
	width: 48%;
	height: 120px;
	margin-bottom: 40px;
	text-align: center;
}
.public-list image {
	width: 100%;
	height: 120px;
	padding-bottom: 5px;
}
.public-list text {
	font-size: 14px;
	color: #333;
}
.tip-box {
	font-size: 25px;
	font-weight: 600;
	text-align: center;
	margin-top: 15px;
}
.color-btn {
	color: #ed7c06;
}
</style>
