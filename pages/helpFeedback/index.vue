<template>
  <view>
    <navBar
      :navBackgroundColor="'#FFFFFF'"
      titleContent="帮助与反馈"
      fontSize="14"
    ></navBar>

    <view class="flex flex-column px-15">
      <view class="pt-20 fs-14 text-3D">常见问题</view>
      <view class="mt-10 rounded-14 bg-white">
        <uv-collapse :border="false" :clickable="false">
          <uv-collapse-item
            title="识别二维码提示“无法找到该用户，请检查你填写的 账号是否正确。”该怎么处理?"
            name="Docs guide"
          >
            <text class="uv-collapse-content">
              识别二维码提示“无法找到该用户，请检查你填写的
              账号是否正确。”该怎么处理?
            </text>
            <view
              class="position-absolute top-13 left-0 bg-green-2 w-4 h-13"
            ></view>
          </uv-collapse-item>
          <uv-line></uv-line>
          <uv-collapse-item
            title="账号之前已开通权限，但再次登录又提示需要重新开通?"
            name="Variety components"
          >
            <text class="uv-collapse-content">
              账号之前已开通权限，但再次登录又提示需要重新开通?
            </text>
            <view
              class="position-absolute top-13 left-0 bg-green-2 w-4 h-13"
            ></view>
          </uv-collapse-item>
          <uv-line></uv-line>
          <uv-collapse-item
            title="手机验证码登录无法收到验证码?"
            name="Numerous tools"
          >
            <text class="uv-collapse-content">
              众多JS小工具，是您开发过程中召之即来的利器，让您飞镖在手，百步穿杨
            </text>
            <view
              class="position-absolute top-13 left-0 bg-green-2 w-4 h-13"
            ></view>
          </uv-collapse-item>
          <uv-line></uv-line>
          <uv-collapse-item
            title="如何查看历史考试记录??"
            name="Numerous tools"
          >
            <text class="uv-collapse-content">
              众多JS小工具，是您开发过程中召之即来的利器，让您飞镖在手，百步穿杨
            </text>
            <view
              class="position-absolute top-13 left-0 bg-green-2 w-4 h-13"
            ></view>
          </uv-collapse-item>
        </uv-collapse>
      </view>
    </view>

    <view
      class="w-p-100 h-52 bg-white flex flex-y-center flex-x-center position-fixed right-0 bottom-0"
    >
      <view
        class="w-168 h-36 fs-15 leading-36 text-center rounded-22 bg-grey-8 text-white fs-14 text-grey-8"
      >
        我要反馈
      </view>
    </view>
  </view>
</template>

<script setup></script>

<style lang="scss" scoped>
.uv-collapse-item {
  position: relative !important;
}
</style>
