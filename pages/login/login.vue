<template>
	<view>
		<view class="title-box"><uni-title title1="登录" title2="朝夕" text1="视频课资源下载" /></view>

		<form>
			<view class="item">
				<view class="label">QQ</view>
				<input v-model="loginData.name" type="text" placeholder="请输入QQ" />
			</view>

			<view class="item">
				<view class="label">密码</view>
				<input v-model="loginData.password" type="password" password="true" placeholder="请输入密码" />
			</view>

			<view class="item">
				<view class="label">验证码</view>
				<input v-model="loginData.imgCode" type="text" placeholder="请输入验证码" />
				<image @click="getImgCode" :src="'https://test.zhaoxiedu.net/api/login/CreateValidateCode/?t=' + imgCode" mode="" />
			</view>

			<view class="item"><button type="primary" @click="subFun">登录</button></view>
		</form>

		<view class="item">
			<view class="tip-text"><text @click="goReg">暂无账号，我要注册</text></view>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			imgCode: +new Date(),
			loginData: {
				name: '',
				password: '',
				imgCode: ''
			}
		};
	},
	methods: {
		getImgCode() {
			this.imgCode = +new Date();
		},
		subFun() {
			let msg = '';
			if (!this.loginData.imgCode || this.loginData.imgCode.length != 4) {
				msg = '请输入正确格式的验证码';
			}
			if (!this.loginData.password || this.loginData.password.length < 5) {
				msg = '请输入正确的密码';
			}
			if (!this.loginData.name || this.loginData.name.length < 6) {
				msg = '请输入正确格式的帐号';
			}

			if (!msg) {
				uni.request({
					url: 'https://www.fastmock.site/mock/b5b84dc2a6df42eb062ed5ee7bd72b4a/uni/login',
					data: this.loginData,
					method: 'POST',
					success: res => {
						uni.setStorage({
							key: 'token',
							data: res.data.data,
							success: function() {
								uni.switchTab({ url: '/pages/index/index' });
							}
						});
					}
				});
			} else {
				uni.showToast({
					title: msg,
					duration: 1000,
					icon: 'none'
				});
			}
		},
    goReg() {
      uni.navigateTo({
        url: `/pages/register/register`,
      });
    }
	}
};
</script>

<style scoped>
/* #ifdef APP-PLUS */
.title-box {
	padding: 30px 0px;
}
/* #endif */

.item {
	height: 50px;
	display: flex;
	align-items: center;
	flex-direction: row;
	padding: 0 10px;
	border-top: 2px solid #efefef;
}
.item .label {
	width: 100px;
}
.item image {
	width: 100px;
	height: 40px;
}
.item input {
	flex: 1;
}
.item button {
	width: 100%;
	margin-top: 20px;
}
.tip-text {
	width: 100%;
	text-align: right;
	color: #333;
}
.tip-text text {
	text-decoration: underline;
}
</style>
