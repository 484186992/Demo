<template>
  <view>
    <web-view :src="url" />
  </view>
</template>

<script>
export default {
  data() {
    return {
      url: "",
    };
  },
  onLoad(option) {
    console.log(option);
    this.url = option.url;
    // this.url = "https://www.zhaoxiedu.net/#/";
    uni.setNavigationBarTitle({ title: option.title });
  },
  methods: {},
};
</script>

<style></style>
