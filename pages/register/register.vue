<template>
	<view>
		<view class="title-box"><uni-title title1="注册" title2="朝夕" text1="VIP学员可获取对应课程的视频源码" /></view>

		<form>
			<view class="item">
				<view class="label">昵称</view>
				<input v-model="loginData.username" type="text" placeholder="请输入昵称" />
			</view>

			<view class="item">
				<view class="label">QQ</view>
				<input v-model="loginData.name" type="text" placeholder="请输入QQ" />
			</view>

			<view class="item">
				<view class="label">手机号</view>
				<input v-model="loginData.phone" type="text" placeholder="请输入手机号" />
			</view>

			<view class="item">
				<view class="label">性别</view>
				<picker :range="array" :value="sex" @change="getSex">
					<view class="uni-input">{{ array[sex] }}</view>
				</picker>
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

			<view class="item"><button type="primary" @click="subFun">注册</button></view>
		</form>

		<view class="item">
			<view class="tip-text"><text @click="goLogin">已有账号，我要登录</text></view>
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
				imgCode: '',
				username: '',
				phone: '',
				sex: ''
			},
			array: ['男', '女'],
			sex: 0
		};
	},
	methods: {
		getImgCode() {
			this.imgCode = +new Date();
		},
		subFun() {
			let msg = '';

			this.loginData.sex = this.array[this.sex];
			for (let s in this.loginData) {
				if (!this.loginData[s]) {
					msg = '信息不完整';
				}
			}

			if (!msg) {
				uni.request({
					url: 'https://www.fastmock.site/mock/b5b84dc2a6df42eb062ed5ee7bd72b4a/uni/login',
					data: this.loginData,
					method: 'POST',
					success: res => {
						uni.showToast({
							title: '注册成功',
							duration: 1000,
							icon: 'none'
						});
						// uni.setStorage({
						// key: "token",
						// data: res.data.data,
						// success: function () {
						uni.switchTab({ url: '/pages/home/home' });
						// },
						// });
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
		goLogin() {
			uni.navigateTo({
				url: `/pages/login/login`
			});
		},
		getSex(index) {
			// console.log(index.detail.value);
			this.sex = index.detail.value;
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
