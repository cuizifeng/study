<script setup>
import {
  onLaunch,
  onShow,
  onHide,
  onError,
  onPageNotFound,
} from "@dcloudio/uni-app";
import { checkForUpdate, getSystemInfo } from "@/utils";
import { provide } from "vue";

const globalData = {
  statusBarHeight: "",
  navHeight: "",
  navigationBarHeight: "",
  customHeight: "",
  scaleFactor: "",
  menubarLeft: "",
  windowWidth: "",
};

onLaunch(() => {
  console.log("App Launch");
  // #ifdef MP-WEIXIN
  checkForUpdate();
  // #endif

  /* 获取设备信息 */
  const SystemInfomations = getSystemInfo();
  /* 通用平台 */
  globalData.statusBarHeight = SystemInfomations.statusBarHeight; //状态栏高度
  globalData.scaleFactor = SystemInfomations.scaleFactor; //比例系数
  globalData.windowWidth = SystemInfomations.windowWidth; //当前设备的屏幕宽度
  /* 微信小程序平台 */
  // #ifdef MP-WEIXIN
  globalData.navHeight =
    SystemInfomations.navHeight + SystemInfomations.statusBarHeight; //头部导航栏总高度
  globalData.navigationBarHeight = SystemInfomations.navHeight; //头部导航栏高度
  globalData.customHeight = SystemInfomations.menuButtonHeight; //胶囊高度
  globalData.menubarLeft = SystemInfomations.menuButtonLeft; //胶囊左边界距离左上角的距离
  // #endif
});

onShow(() => {
  console.log("App Show");
});

onHide(() => {
  console.log("App Hide");
});

onError((error) => {
  console.error("App Error", error);
});

onPageNotFound((res) => {
  console.error("PageNotFound", res);
  uni.redirectTo({
    url: "/pages/404/404",
  });
});

provide("globalData", globalData);
</script>

<style lang="scss">
/* 每个页面公共css */
@import "static/page.scss";
@import "static/color.scss";

/* #ifdef MP-WEIXIN */

/* #endif */

/* #ifndef MP-WEIXIN */
@font-face {
  font-family: "SimSun"; // 引入字体包，自己起的名字
  src: url("/static/font/simsun.ttf"); // 字体包本地路径
}
/* #endif */

/* uv-ui基础样式 */
@import "@/uni_modules/uv-ui-tools/index.scss";
</style>

<style>
page {
  height: 100%;
  background: #fafafa;
  font-family: SimSun;
}
</style>
