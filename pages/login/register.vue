<template>
  <view>
    <navBar :navBackgroundColor="'#FFFFFF'"></navBar>

    <stepBar step="2"></stepBar>
    <view class="h1">手机验证登录</view>
    <view class="h2">未注册的手机号码验证后将自动创建账号</view>

    <!-- 用户手机号 -->
    <!-- <view>
      <view class="inpText">
        <view class="_item">
          <view class="name">真实姓名</view>
          <uv-input
            placeholder="请输入内容"
            border="none"
            :customStyle="{ paddingLeft: '23px' }"
            clearable
          ></uv-input>
        </view>

        <view class="_item card">
          <view class="name">身份证</view>
          <uv-input
            placeholder="请输入内容"
            border="none"
            :customStyle="{ paddingLeft: '37px' }"
            clearable
          ></uv-input>
        </view>
      </view>
      <view class="h3">信息仅用于身份验证，严格保密</view>
    </view> -->

    <!-- 上传身份证 -->
    <!-- <view class="uploadImg">
      <view class="z"></view>
      <view class="tip">照片需清晰、无遮挡</view>
      <view class="f"></view>
    </view> -->

    <!-- 人脸认证 -->
    <view class="face">
      <view class="_video"></view>
      <view class="_tip">
        <view class="_item">
          <view class="img"></view>
          <view class="_t">避免遮挡</view>
        </view>
        <view class="_item">
          <view class="img"></view>
          <view class="_t">光线充足</view>
        </view>
        <view class="_item">
          <view class="img"></view>
          <view class="_t">动作过快</view>
        </view>
      </view>
    </view>

    <view class="footbar">
      <view class="code active">上传身份证照片</view>
      <view class="code">先等等</view>
      <view class="code active">人脸验证</view>
      <view class="code active" @click="startVerify">开始验证</view>
    </view>
  </view>
</template>

<script setup>
import { ref } from "vue";
const startVerify = () => {
  uni.navigateTo({
    url: "/pages/login/supplementaryFile",
  });
};
</script>

<style lang="scss" scoped>
.h1 {
  font-size: 26px;
  font-weight: 600;
  color: #3d3d3d;
  padding-left: 15px;
  padding-top: 13px;
}
.h2 {
  font-size: 14px;
  font-weight: 500;
  color: #6b7280;
  padding-left: 15px;
  padding-top: 12px;
}
.inpText {
  padding: 47px 15px 0 15px;
  display: flex;
  flex-direction: column;
  ._item {
    height: 48px;
    padding: 0px 22px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #f5f5f5;
    border-radius: 25px;
    .name {
      font-size: 14px;
      color: #1d2129;
    }
  }
  .card {
    margin-top: 24px;
  }
}
.h3 {
  font-size: 14px;
  color: #3d3d3d;
  padding-top: 17px;
  padding-left: 15px;
}
.footbar {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: fixed;
  left: 0px;
  bottom: 92px;
  .code {
    width: 345px;
    height: 44px;
    line-height: 44px;
    text-align: center;
    background: #c9cdd4;
    border-radius: 22px;
    color: #fafafa;

    font-size: 18px;
    font-weight: 500;
    margin-top: 18px;
  }
  .active {
    background: #1cd1de;
  }
}

.uploadImg {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  .z {
    width: 301px;
    height: 171px;
    border: 1rpx solid #1cd1de;
    border-radius: 15px;
  }
  .tip {
    width: 301px;
    text-align: left;
    color: #3d3d3d;

    font-size: 12px;
  }
  .f {
    width: 301px;
    height: 171px;
    border: 1rpx solid #1cd1de;
    border-radius: 15px;
  }
}

.face {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 34px;
  ._video {
    width: 148px;
    height: 148px;
    border: 1px solid #1cd1de;
  }
  ._tip {
    margin-top: 27px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    ._item {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 0px 27px;
      .img {
        width: 57px;
        height: 57px;
        border: 1px solid #1cd1de;
      }
      ._t {
        margin-top: 12px;
        font-size: 14px;
        color: #3d3d3d;
      }
    }
  }
}
</style>
