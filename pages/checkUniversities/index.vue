<template>
  <view>
    <customizeBar navBackgroundColor="#FFFFFF" :lintHeight="112">
      <view class="h-p-100 flex flex-column">
        <view
          class="px-19 flex flex-y-center flex-x-space-between"
          style="flex: 1"
        >
          <view class="flex flex-y-center">
            <uv-icon name="arrow-left"></uv-icon>
            <view class="pl-10 fs-14 text-3D">查院校</view>
          </view>
          <view class="flex flex-y-center">
            <view class="pr-6 fs-12 text-3D">筛选</view>
            <uv-icon name="search"></uv-icon>
          </view>
        </view>
        <view class="h-56 px-15 flex flex-y-center flex-x-space-between">
          <view
            class="w-280 h-32 flex flex-y-center px-17 rounded-17 bg-grey-9"
          >
            <uv-icon name="search"></uv-icon>
            <input class="pl-11 fs-12" placeholder="请输入院校名称搜索" />
          </view>
          <view class="fs-12 text-3D">搜索</view>
        </view>
      </view>
    </customizeBar>

    <view class="p-15">
      <view class="flex flex-column bg-white rounded-14 px-15 py-5 pb-10">
        <view
          class="h-100 flex flex-y-center bg-grey-10 mt-15 rounded-8 px-15"
          v-for="(item, i) in 3"
          :key="i"
        >
          <view>
            <image
              class="w-60 h-60 rounded-50"
              src="https://img0.baidu.com/it/u=2229144304,3578627907&fm=253&fmt=auto&app=138&f=JPEG?w=467&h=300"
            ></image>
          </view>
          <view class="pl-10">
            <view class="fs-14 text-3D text-ellipsis-1">
              渤海理工职业学院渤海理工职业学院渤海理工职业学院
            </view>
            <view class="flex flex-y-center fs-10 text-grey-8 py-7">
              <view class="py-2 px-5 bg-green-4 rounded-2 text-green-2 mr-5">
                双高
              </view>
              <view class="py-2 px-5 bg-grey-6 rounded-2 text-green-8 mr-5">
                综合类
              </view>
              <view class="py-2 px-5 bg-grey-6 rounded-2 text-green-8 mr-5">
                公办
              </view>
              <view class="py-2 px-5 bg-grey-6 rounded-2 text-green-8">
                国家级骨干
              </view>
            </view>
            <view class="fs-10 text-3D flex flex-y-center">
              <uv-icon name="map" color="#1CD1DE"></uv-icon>
              <text class="text-ellipsis-1 pl-5">
                重庆市沙坪坝区大学城南二路151号重庆市沙坪坝区大学城南二路151号
              </text>
            </view>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup></script>

<style lang="scss" scoped></style>
