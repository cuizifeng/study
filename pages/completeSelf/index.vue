<template>
  <view>
    <navBar :navBackgroundColor="'#FFFFFF'"></navBar>
    <view class="flex flex-column flex-y-center">
      <view class="my-22">
        <image
          class="rounded-20 w-146 h-146"
          src="https://img1.baidu.com/it/u=257341075,3427834616&fm=253&fmt=auto&app=138&f=JPEG?w=737&h=500"
        ></image>
      </view>
      <view class="fs-18 text-3D">恭喜你！</view>
      <view class="fs-18 text-3D mt-10">已完成 语文 摸底自测</view>
      <view class="fs-14 mt-15" style="color: #6b7280">
        还差一步，即可生成完整评估报告
      </view>
      <view
        style="color: #fafafa"
        class="w-285 h-44 bg-green-2 mt-91 leading-44 text-center rounded-35 fs-18"
      >
        继续完成综合问答
      </view>
    </view>
  </view>
</template>

<script setup></script>

<style lang="scss" scoped>
page {
  background: #ffffff;
}
.img {
  width: 292rpx;
  height: 292rpx;
}
</style>
