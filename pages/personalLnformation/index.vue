<template>
  <view>
    <navBar
      :navBackgroundColor="'#FFFFFF'"
      titleContent="个人信息"
      fontSize="14"
    ></navBar>

    <view class="flex flex-column">
      <uv-gap height="10"></uv-gap>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">头像</view>
        <view>
          <image
            class="w-32 h-32 rounded-50"
            src="https://q1.itc.cn/q_70/images03/20250129/4d820c22829549d9a2008243b262458f.jpeg"
          ></image>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">昵称</view>
        <view class="flex flex-y-center">
          <view class="fs-14 text-grey-7 pr-15">155****1234</view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-gap height="10"></uv-gap>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">绑定手机号</view>
        <view class="flex flex-y-center">
          <view class="fs-14 text-grey-7 pr-15">155****1234</view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">绑定微信</view>
        <view class="flex flex-y-center">
          <view class="fs-14 text-grey-7 pr-15">未绑定</view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
    </view>

    <view
      class="w-p-100 h-52 bg-white flex flex-y-center flex-x-center position-fixed right-0 bottom-0"
    >
      <image class="w-20 h-20" src="/static/pageImg/close.png"></image>
      <view class="pl-25 fs-15 text-grey-8">退出登录</view>
    </view>
  </view>
</template>

<script setup></script>

<style lang="scss" scoped></style>
