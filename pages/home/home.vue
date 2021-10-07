<template>
  <view>
    <swiper
      class="home-swiper"
      indicator-dots="true"
      :interval="2000"
      autoplay="true"
      circular="true"
    >
      <swiper-item v-for="(i, index) in list" :key="index">
        <view class="swiper-item uni-bg-red">
          <image :src="i" mode="scaleToFill" />
        </view>
      </swiper-item>
    </swiper>

    <uni-title
      @getTitle="getTitleFun($event)"
      title1="朝夕名师"
      title2="在线直播"
      text1="直播互动学习，感受技术韵律"
    />

    <view class="public-box">
      <view
        @click="goPublic(i.url, i.text)"
        class="public-list"
        v-for="i in publicList"
        :key="i.url"
      >
        <image :src="i.img" mode="" />
        <text>{{ i.text }}</text>
      </view>
    </view>

    <uni-title
      @getTitle="getTitleFun($event)"
      title1="加入"
      title2="朝夕"
      text1="让每个人的职业生涯不留遗憾"
    />
    <view class="recruitSmall-box">
      <view v-for="(i, index) in recruitSmall" :key="index" class="recruitSmall-list">
        <image :src="i.img" mode="" />
        <view class="recruitSmall-text-box">
          <text class="recruitSmall-text-title">{{ i.title }}</text>
          <text>{{ i.text }}</text>
        </view>
      </view>
    </view>

    <uni-title
      @getTitle="getTitleFun($event)"
      title1="合作"
      title2="伙伴"
      text1="人生道路上伙伴的支撑不可或缺"
    />
    <view class="buddy-box">
      <image v-for="i in buddy" :key="i.img" :src="i.img" class="buddy-list" mode="" />
    </view>

  </view>
</template>

<script>
export default {
  data() {
    return {
      list: [
        "https://www.zhaoxiedu.net/static/imgs/carousel/%E8%BD%AE%E6%92%AD-3-%E5%85%A8%E6%A0%88.jpg",
        "https://www.zhaoxiedu.net/static/imgs/carousel/%E8%BD%AE%E6%92%AD-3-%E5%85%A8%E6%A0%88.jpg",
        "https://www.zhaoxiedu.net/static/imgs/carousel/%E8%BD%AE%E6%92%AD-3-%E5%85%A8%E6%A0%88.jpg",
        "https://www.zhaoxiedu.net/static/imgs/carousel/%E8%BD%AE%E6%92%AD-3-%E5%85%A8%E6%A0%88.jpg",
      ],
      publicList: [],
      recruitSmall: [],
      buddy: [],
    };
  },
  onLoad() {
    uni.request({
      url: "https://www.fastmock.site/mock/b5b84dc2a6df42eb062ed5ee7bd72b4a/uni/getCouesel",
      success: (res) => {
        // this.list = res.data.data;
        console.log(res.data);
      },
    });
    uni.request({
      url: "https://www.fastmock.site/mock/b5b84dc2a6df42eb062ed5ee7bd72b4a/uni/getPublic",
      success: (res) => {
        this.publicList = res.data.data;
        // console.log(res.data);
      },
    });
    uni.request({
      url: "https://www.fastmock.site/mock/b5b84dc2a6df42eb062ed5ee7bd72b4a/uni/getRecruitSmall",
      success: (res) => {
        this.recruitSmall = res.data.data;
        // console.log(res.data);
      },
    });
    uni.request({
      url: "https://www.fastmock.site/mock/b5b84dc2a6df42eb062ed5ee7bd72b4a/uni/getBuddy",
      success: (res) => {
        this.buddy = res.data.data;
        // console.log(res.data);
      },
    });
  },
  methods: {
    getTitleFun(text) {
      console.log(text);
    },
    goPublic(url, title) {
      // console.log(url);
      uni.navigateTo({
        url: `/pages/publicView/publicView?url=${url}&title=${title}`,
      });
    },
  },
};
</script>

<style scoped>
.swiper-item {
  width: 100%;
  height: 100%;
}
.swiper-item image {
  width: 100%;
  height: 100%;
}
.public-box,
.buddy-box {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
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
.recruitSmall-box {
  padding: 10px;
}
.recruitSmall-list {
  display: flex;
  flex-direction: row;
  margin-bottom: 10px;
}
.recruitSmall-list image {
  width: 40%;
  height: 120px;
  margin-right: 10px;
  border-radius: 10px;
}
.recruitSmall-text-box {
  flex: 1;
  display: flex;
  flex-direction: column;
  color: #333;
  font-size: 14px;
}
.recruitSmall-text-title {
  font-weight: 600;
  margin: 5px 0;
  font-size: 16px;
}
.buddy-list {
  width: 30%;
  height: 60px;
}
</style>
