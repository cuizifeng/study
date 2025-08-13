<template>
  <view>
    <customizeBar navBackgroundColor="#FFFFFF">
      <view class="pageTitle">
        <view class="_right">
          <uv-icon name="arrow-left" size="18px" color="#1d2129"></uv-icon>
        </view>
        <view class="_left">
          <uv-icon name="clock" size="18px" color="#6B7280"></uv-icon>
          <view class="countDown">
            <uv-count-down
              :time="30 * 60 * 1000"
              format="mm:ss"
              :customStyle="{
                color: '#6B7280',
              }"
            ></uv-count-down>
          </view>
          <uv-icon name="question-circle" size="18px" color="#6B7280"></uv-icon>
        </view>
      </view>
    </customizeBar>
  </view>
</template>

<script setup></script>

<style lang="scss" scoped>
.pageTitle {
  height: 100%;
  padding: 0rpx 30rpx;
  display: flex;
  align-items: center;
  /* #ifndef MP-WEIXIN */
  justify-content: space-between;
  /* #endif */
  ._right {
    display: flex;
    align-items: center;
    .h4 {
      font-size: 36rpx;
      color: #1d2129;
    }
    .category {
      font-size: 28rpx;
      font-weight: 350;
      color: #1d2129;
      padding-left: 26rpx;
      padding-right: 16rpx;
    }
  }
  ._left {
    display: flex;
    align-items: center;
    padding-left: 16rpx;
    .countDown {
      width: 120rpx;
    }
    .city {
      font-size: 24rpx;
      font-weight: 350;
      color: #3d3d3d;
      padding-left: 10rpx;
    }
  }
}
</style>
