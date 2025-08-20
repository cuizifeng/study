<template>
  <view>
    <customizeBar navBackgroundColor="rgba(255, 255, 255, 0)"></customizeBar>
    <view class="bg-fixed"></view>
    <view class="px-16">
      <view class="flex flex-y-center flex-x-space-between">
        <view class="flex flex-y-center">
          <view>
            <image
              class="w-64 h-64 rounded-50"
              src="https://m.tuniucdn.com/fb2/t1/G5/M00/44/52/Cii-s1soezyIF2UxABn76u-yKl8AAIwBgB34jAAGfwC3020871"
            ></image>
          </view>
          <view class="pl-15 fs-16 text-white" style="z-index: 1">
            15099999999
          </view>
        </view>
        <view class="flex flex-y-center">
          <view>
            <uv-icon size="20" color="#FFFFFF" name="scan"></uv-icon>
          </view>
          <view class="ml-15" @click="setting">
            <uv-icon size="20" color="#FFFFFF" name="setting"></uv-icon>
          </view>
        </view>
      </view>

      <view
        class="w-325 h-88 mx-auto rounded-top-left-14 rounded-top-right-14 mt-20 flex flex-y-center flex-x-space-between"
        style="background: rgba(251, 248, 253, 0.55)"
      >
        <view class="ml-10">
          <image
            class="w-90 h-53"
            src="https://m.tuniucdn.com/fb2/t1/G5/M00/44/52/Cii-s1soezyIF2UxABn76u-yKl8AAIwBgB34jAAGfwC3020871"
          ></image>
        </view>
        <view class="flex flex-column px-8">
          <view class="fs-12 text-3D">
            您是SVIP会员，享有全部真题题库和课程视频权限
          </view>
          <view class="fs-12 fw-350 text-grey-7 pt-6">
            有效期至2026年8月1日
          </view>
        </view>
      </view>

      <view
        class="h-54 flex flex-y-center flex-x-space-between rounded-14 bg-white px-13"
      >
        <view class="flex flex-y-center">
          <image class="w-28 h-28" src="/static/pageImg/my-hui.png"></image>
          <view class="fs-16 text-3D pl-10">我的系统提分课程</view>
        </view>
        <view>
          <image class="w-18 h-18" src="/static/pageImg/my-hui.png"></image>
        </view>
      </view>

      <view
        class="w-p-100 flex flex-y-center flex-wrap flex-x-space-between rounded-14 bg-white mt-15 pb-19"
      >
        <view class="w-p-25 mt-19" v-for="(item, i) in navList" :key="i">
          <view class="flex flex-column flex-y-center">
            <view
              class="w-48 h-48 rounded-50 bg-green-3 flex flex-y-center flex-x-center"
            >
              {{ i }}
            </view>
            <view class="fs-14 text-3D pt-5">{{ item.name }}</view>
          </view>
        </view>
      </view>

      <view class="flex flex-column bg-white rounded-14 mt-15 p-15">
        <view class="flex flex-y-center flex-x-space-between">
          <view class="fs-14 text-grey-8">报考年份</view>
          <view class="flex flex-y-center">
            <view class="px-15 py-2 rounded-8 bg-green-4 fs-14 text-green-2">
              2026
            </view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
        <view class="flex flex-y-center flex-x-space-between mt-27">
          <view class="fs-14 text-grey-8">我的身份</view>
          <view class="flex flex-y-center">
            <view class="fs-14 text-grey-7">学生</view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
        <view class="flex flex-y-center flex-x-space-between mt-27">
          <view class="fs-14 text-grey-8">就读学校</view>
          <view class="flex flex-y-center">
            <view class="fs-14 text-grey-7">选择</view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
        <uv-line color="#F0F0F0" margin="28rpx 0rpx 0rpx 0rpx"></uv-line>
        <view class="flex flex-y-center flex-x-space-between mt-14">
          <view class="fs-14 text-grey-8">分享好友</view>
          <view class="flex flex-y-center">
            <uv-icon name="question-circle"></uv-icon>
          </view>
        </view>
        <view class="flex flex-y-center flex-x-space-between mt-27">
          <view class="fs-14 text-grey-8">帮助/反馈</view>
          <view class="flex flex-y-center">
            <uv-icon name="question-circle"></uv-icon>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from "vue";
const navList = ref([
  {
    name: "个人档案",
    img: "",
  },
  {
    name: "错题本",
    img: "",
  },
  {
    name: "我的订单",
    img: "",
  },
  {
    name: "作业/考试",
    img: "",
  },
  {
    name: "测试",
    img: "",
  },
]);

const setting = () => {
  console.log("======");
  uni.navigateTo({
    url: "/pages/setUp/index",
  });
};
</script>

<style lang="scss" scoped>
/* #ifdef H5 */
page,
  /* #endif */
    /* #ifndef H5 */
    .bg-fixed
     /* #endif */ {
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  /* #ifndef H5 */
  z-index: -1;
  /* #endif */
  background-image: linear-gradient(
    172deg,
    rgba(89, 152, 247, 0.6) 5%,
    rgba(247, 136, 182, 0.15) 60%,
    rgba(247, 136, 182, 0) 100%
  );
}
</style>
