<template>
  <view>
    <image
      src="https://m.zhaoxiedu.net/img/%E8%AF%BE%E7%A8%8B%E4%B8%AD%E5%BF%83.4ec05eec.jpg"
      class="banner-img"
      mode="widthFix"
    />
    <view class="list">
      <view v-for="(i, index) in course" :key="index" class="course-list">
        <text class="course-title">{{ i.courseName }}</text>
        <view class="course-content">
          <image :src="i.img" mode="widthFix" class="course-img" />
          <view class="course-text">
            <text>{{ i.describe }}</text>
            <navigator :url="`/pages/publicView/publicView?url=${i.url}&title=${i.courseName}`">
              <button type="default" size="mini" class="btn">查看详情</button>
            </navigator>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      course: [],
    };
  },
  methods: {},
  onLoad() {
    uni.request({
      url: "https://www.fastmock.site/mock/b5b84dc2a6df42eb062ed5ee7bd72b4a/uni/getCourse",
      success: (res) => {
        this.course = res.data.data;
      },
    });
  },
};
</script>

<style scoped>
.banner-img {
  width: 100%;
  /* height: 130px; */
}
.course-list {
  padding: 10px;
  text-align: center;
}
.course-content {
  display: flex;
  flex-direction: row;
  width: 100%;
  margin-top: 10px;
}
.course-img {
  width: 40%;
  margin-right: 5px;
}
.course-text {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  text-align: left;
}
.course-text text {
  font-size: 14px;
}
.btn {
  color: #fff;
  background-color: rgb(238, 159, 32);
  border-color: rgb(238, 159, 32);
}
</style>
