<template>
  <view class="container">
    <navBar :navBackgroundColor="'#FFFFFF'"></navBar>

    <stepBar></stepBar>
    <view class="h1">手机验证登录</view>
    <view class="h2">未注册的手机号码验证后将自动创建账号</view>

    <view>
      <view class="inpText">
        <view class="_item">
          <view class="name">+86</view>
          <uv-input
            placeholder="请输入内容"
            border="none"
            :customStyle="customStyle"
            clearable
          ></uv-input>
        </view>
      </view>

      <view class="tips">
        <view>
          <uv-checkbox-group v-model="checkboxValue">
            <uv-checkbox
              :customStyle="{}"
              v-for="(item, index) in checkboxList"
              :key="index"
              :label="item.name"
              :name="item.name"
              labelColor="#6B7280"
              labelSize="12"
              inactiveColor="#9CA3AF"
              activeColor="#1CD1DE"
              size="14"
            ></uv-checkbox>
          </uv-checkbox-group>
        </view>

        <view class="_item">《用户服务协议》</view>
        <view class="_item">《隐私政策》</view>
      </view>
    </view>

    <view style="padding-top: 59px">
      <view class="inpCode">
        <uv-code-input
          mode="line"
          :maxlength="6"
          :hairline="true"
        ></uv-code-input>
      </view>
      <view class="u-demo-block__content">
        <uv-code
          ref="uCode2"
          @change="codeChange2"
          keep-running
          start-text="点我获取验证码"
          seconds="60"
        ></uv-code>
        <text @tap="getCode2" :text="tips2" class="u-page__code-text">
          {{ tips2 }}
        </text>
      </view>
    </view>

    <view class="code" @click="getCode">获取验证码</view>
    <!-- <view>
      <uv-button type="primary" text="注册" @click="handleRegister"></uv-button>
      <uv-button type="success" text="登录" @click="handleLogin"></uv-button>
    </view> -->
  </view>
</template>

<script setup>
import { ref } from "vue";
import {
  HOME_PATH,
  LOGIN_PATH,
  isTabBarPath,
  removeQueryString,
} from "@/router";
import { useAuthStore } from "@/store";
import { onLoad } from "@dcloudio/uni-app";

let redirect = HOME_PATH;
onLoad((options) => {
  if (options.redirect && removeQueryString(options.redirect) !== LOGIN_PATH) {
    redirect = decodeURIComponent(options.redirect);
  }
});
const customStyle = ref({
  paddingLeft: "24px",
});

const checkboxValue = ref([]);
const checkboxList = ref([
  {
    name: "我已阅读并同意",
    disabled: false,
  },
]);

const tips2 = ref("");
const uCode2 = ref();

const codeChange2 = (text) => {
  tips2.value = text;
};

const getCode2 = () => {
  if (uCode2.value.canGetCode) {
    // 模拟向后端请求验证码
    uni.showLoading({
      title: "正在获取验证码",
    });
    setTimeout(() => {
      uni.hideLoading();
      // 这里此提示会被this.start()方法中的提示覆盖
      uni.$uv.toast("验证码已发送");
      // 通知验证码组件内部开始倒计时
      uCode2.value.start();
    }, 2000);
  } else {
    uni.$uv.toast("倒计时结束后再发送");
  }
};

const authStore = useAuthStore();

async function handleRegister() {
  await authStore.signUp({
    username: "visitor",
    password: "123456",
  });
  uni.$uv.toast("注册成功");
  setTimeout(() => {
    uni.$uv.route({
      type: isTabBarPath(redirect) ? "switchTab" : "redirectTo",
      url: redirect,
    });
  }, 800);
}

async function handleLogin() {
  await authStore.signIn({
    username: "visitor",
    password: "123456",
  });
  uni.$uv.toast("登录成功");
  setTimeout(() => {
    uni.$uv.route({
      type: isTabBarPath(redirect) ? "switchTab" : "redirectTo",
      url: redirect,
    });
  }, 800);
}

const getCode = () => {
  uni.navigateTo({
    url: "/pages/login/register",
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
  ._item {
    height: 48px;
    padding: 0px 14px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #f5f5f5;
    border-radius: 25px;
    .name {
      color: #9ca3af;
    }
  }
}
.tips {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 20px;
  padding-top: 7px;

  ._item {
    font-size: 12px;
    color: #1cd1de;
  }
}
.inpCode {
  display: flex;
  align-items: center;
  justify-content: center;
}
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
  margin: 89px auto;
}
.uv-code-input {
  width: 375px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.u-demo-block__content {
  display: flex;
  flex-direction: row-reverse;
  padding-top: 10px;
  padding-right: 15px;
  color: #1cd1de;

  font-size: 12px;
}
</style>
