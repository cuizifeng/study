<template>
  <view>
    <navBar
      :navBackgroundColor="'#FFFFFF'"
      titleContent="设置"
      fontSize="14"
    ></navBar>

    <view class="flex flex-column">
      <uv-gap height="10"></uv-gap>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">个人信息</view>
        <view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">考试时间</view>
        <view class="flex flex-y-center">
          <view class="fs-14 text-grey-7 pr-15">请设置考试时间</view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-gap height="10"></uv-gap>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">版本更新</view>
        <view class="flex flex-y-center">
          <view class="fs-14 text-grey-7 pr-15">目前是最新版本v1.0.0</view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">用户协议</view>
        <view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">隐私设置</view>
        <view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">个人信息清单</view>
        <view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">第三方共享清单</view>
        <view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">个人信息保护设置</view>
        <view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
      <uv-line color="#E5E5E5"></uv-line>
      <view
        class="bg-white h-52 pl-15 pr-20 flex flex-y-center flex-x-space-between"
      >
        <view class="fs-14 text-grey-8">备案号</view>
        <view class="flex flex-y-center">
          <view class="fs-14 text-grey-7 pr-15">湘ICP备203342423号-2A</view>
          <uv-icon name="arrow-right"></uv-icon>
        </view>
      </view>
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
