/* * 注意： *
1、在传入宽度或者高度时，如果是Number数据，传入的值为px大小,无需带单位，组件自动计算
*
2、在使用此导航栏时，建议传入UI规定的导航栏高度，此高度只针对除微信小程序的其他平台有效，微信小程序的导航栏高度，组件自计算
*/
<template>
  <view>
    <!-- 微信小程序头部导航栏 -->
    <!-- #ifdef MP-WEIXIN -->
    <view
      class="wx-head-mod"
      :style="{
        height: navHeight + 'rpx',
        backgroundColor: navBackgroundColor,
      }"
    >
      <view
        class="wx-head-mod-nav"
        :style="{
          height: navigationBarHeight + 'rpx',
          top: statusBarHeight + 'rpx',
        }"
      >
        <slot></slot>
      </view>
    </view>
    <!-- #endif -->

    <!-- 除微信小程序之外的其他设备 -->
    <!-- #ifndef MP-WEIXIN -->
    <view
      class="other-head-mod"
      :style="{
        height: navHeightValue * scaleFactor + statusBarHeight + 'rpx',
        backgroundColor: navBackgroundColor,
      }"
    >
      <view
        class="other-head-mod-mian"
        :style="{
          height: navHeightValue * scaleFactor + 'rpx',
        }"
      >
        <slot></slot>
      </view>
    </view>
    <!-- #endif -->
    <view
      :style="{
        marginTop: navHeightValue * scaleFactor + statusBarHeight + 'rpx',
      }"
    ></view>
  </view>
</template>
<script setup>
import { ref, computed, inject } from "vue";
const props = defineProps({
  // 文本区域位置 left：左  center：中
  textAlign: {
    type: String,
    default: "center",
  },
  // 文本区内容
  titleContent: {
    type: String,
    default: "",
  },
  // 文本区离左边的距离
  textPaddingLeft: {
    type: Number,
    default: 16,
  },
  // 是否需要返回按钮
  isBackShow: {
    type: Boolean,
    default: true,
  },
  // 文本区字体大小
  fontSize: {
    type: Number,
    default: 20, //px
  },
  // 文本区字体粗细
  fontWeight: {
    type: Number,
    default: 500,
  },
  // 文本区返回按钮图片宽
  backImageWidth: {
    type: Number,
    default: 12, //px
  },
  // 文本区返回按钮图片高
  backImageHeight: {
    type: Number,
    default: 24, //px
  },
  // 返回按钮图标路径
  backImageUrl: {
    type: String,
    default: "/static/pageImg/left_jt.png",
  },
  // 导航栏整体背景颜色
  navBackgroundColor: {
    type: String,
    default: "#2476F9",
  },
  // 标题字体颜色
  titleColor: {
    type: String,
    default: "#3D3D3D",
  },

  /******** h5端，app端需要传入自定义导航栏高度 *******/
  navHeightValue: {
    type: Number,
    default: 44, //px
  },
});

const globalData = inject("globalData");

// 文本区宽度
const navTextWidth = computed(() => {
  if (props.textAlign === "center") {
    return (
      windowWidth.value - (windowWidth.value - menubarLeft.value) * 2 + "rpx"
    );
  } else {
    return menubarLeft.value + "rpx";
  }
});
// 文本区paddingLeft
const textPaddingleft = computed(() => {
  if (props.textAlign === "center") {
    return "0";
  } else {
    return props.textPaddingLeft + "rpx";
  }
});

const statusBarHeight = ref(globalData.statusBarHeight); //状态栏高度
const navHeight = ref(globalData.navHeight); //头部导航栏总体高度
const navigationBarHeight = ref(globalData.navigationBarHeight); //导航栏高度
const customHeight = ref(globalData.customHeight); //胶囊高度
const scaleFactor = ref(globalData.scaleFactor); //比例系数
const menubarLeft = ref(globalData.menubarLeft); //胶囊定位的左边left
const windowWidth = ref(globalData.windowWidth * globalData.scaleFactor); //胶囊高度

const backEvent = () => {
  uni.navigateBack();
};
</script>

<style lang="less" scope>
/* #ifdef MP-WEIXIN */
.wx-head-mod {
  box-sizing: border-box;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9;
}

.wx-head-mod-nav {
  box-sizing: border-box;
  width: 100%;
  position: absolute;
  left: 0;
  //   display: flex;
  //   justify-content: center;
  //   align-items: center;
}

/* #endif */

/* #ifndef MP-WEIXIN */
.other-head-mod {
  box-sizing: border-box;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9;
  .other-head-mod-mian {
    position: absolute;
    left: 0;
    bottom: 0;
    box-sizing: border-box;
    width: 100%;
    // display: flex;
    // align-items: center;
    // justify-content: left;
  }
}

/* #endif */
</style>
