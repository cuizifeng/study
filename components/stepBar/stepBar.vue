<template>
  <view class="page-main">
    <view class="step">
      <view class="step-info">
        <view class="step-number">
          <block v-for="(item, index) in stepList" :key="index">
            <view @click.stop="openItem(item)" class="item-state">
              <view
                class="step-id"
                :style="[
                  {
                    background: item.id == step ? checkedColor : unCheckedColor,
                  },
                ]"
              >
                {{ item.id }}
              </view>
            </view>
            <view
              class="line"
              :style="{ background: unCheckedLine }"
              v-if="index < stepList.length - 1"
            ></view>
          </block>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
const props = defineProps({
  //当前步骤
  step: {
    type: [Number, String],
    default: 1,
  },
  //步骤列表
  stepList: {
    type: Array,
    default: () => {
      return [
        {
          name: "第一步",
          id: 1,
        },
        {
          name: "第二步",
          id: 2,
        },
        {
          name: "第三步",
          id: 3,
        },
      ];
    },
  },
  //已完成的字体颜色
  checkedColor: {
    type: String,
    default: "#BBBBBB",
  },
  //未完成的字体颜色
  unCheckedColor: {
    type: String,
    default: "#F4F4F4",
  },
  //已完成的线条颜色
  checkedLine: {
    type: String,
    default: "#BBBBBB",
  },
  //未完成的线条颜色
  unCheckedLine: {
    type: String,
    default: "#F4F4F4",
  },
});

const openItem = (item) => {};
</script>

<style scoped>
.page-main {
  height: auto;
}
.step {
  padding: 0 122rpx;
  padding-top: 13rpx;
}
.step-info {
  width: 100%;
  height: auto;
}

.step-number {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.item-state {
  height: 64rpx;
  display: flex;
  align-items: center;
}

.step-id {
  width: 24px;
  height: 24px;
  line-height: 24px;
  text-align: center;
  border-radius: 50%;
  font-size: 24rpx;
  background: #f4f4f4;
}

.line {
  width: 100%;
  height: 3rpx;
  margin: 0 8rpx;
  background: #d8d8d8;
}
</style>
