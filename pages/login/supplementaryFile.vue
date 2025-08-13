<template>
  <view>
    <navBar :navBackgroundColor="'#FFFFFF'"></navBar>
    <stepBar step="3"></stepBar>

    <view class="title">
      认证成功
      <view class="img"></view>
    </view>
    <view class="h1">补完个人档案，即刻自测</view>
    <view class="h2">完成自测可解锁专属提分学习方案</view>

    <view class="list">
      <view class="item">
        <view class="arrs" @click="open">
          <view class="_left">报考年份</view>
          <view class="_right">
            <view class="year">2026</view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
        <view class="arrs">
          <view class="_left">报考省份</view>
          <view class="_right">
            <view class="_t">河北省</view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
        <view class="arrs">
          <view class="_left">考生类型</view>
          <view class="_right">
            <view class="_t">请选择</view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
        <view class="arrs">
          <view class="_left">报考类别</view>
          <view class="_right">
            <view class="_t">请选择</view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
        <view class="arrs">
          <view class="_left">最近成绩</view>
          <view class="_right">
            <view class="_t">请选择</view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
        <view class="arrs" style="border: none">
          <view class="_left">就读学校</view>
          <view class="_right">
            <view class="_t">请选择</view>
            <uv-icon name="arrow-right"></uv-icon>
          </view>
        </view>
      </view>
    </view>

    <view class="footbar">
      <view class="code active">开始自测</view>
      <view class="code">先等等</view>
    </view>

    <uv-popup ref="popup" mode="bottom" round="14">
      <view class="popBottom">
        <view class="_title">
          <view class="cancel">取消</view>
          <view class="type">预估总分</view>
          <view class="save">保存</view>
        </view>
        <!-- 预估总分 -->
        <!-- <view class="total">
          <view class="h11">请输入最新预估的总成绩区间</view>
          <view class="h55">智能自测试卷会根据成绩自动匹配合适的难度</view>
          <view class="inpNum">
            <view class="inp">
              <input placeholder="输入得分" class="center-input" />
            </view>
            <view class="line"></view>
            <view class="inp">
              <input placeholder="输入得分" class="center-input" />
            </view>
          </view>
        </view> -->

        <!-- 选择省份 -->
        <!-- <view class="province">
          <view class="_title_1">
            <uv-icon name="map"></uv-icon>
            <view class="_in">当前省份</view>
            <view class="city">河北当前省份</view>
          </view>
          <view class="other">其它省份</view>
          <view style="flex: 1">
            <scroll-view scroll-y="true" class="_scroll" style="height: 300px">
              <view class="_scroll_item" v-for="item in 56" :key="item">
                齐齐哈尔
              </view>
            </scroll-view>
          </view>
        </view> -->

        <!-- 考生类型 -->
        <!-- <view class="picker-view-box">
          <picker-view
            :value="candidateType"
            class="picker-view"
            @change="
              (e) => {
                bindChange(e,'candidateType');
              }
            "
          >
            <picker-view-column>
              <view class="item" v-for="(item, index) in columns" :key="index">
                <view :class="[index == candidateType[0] ? 'active' : '']">
                  {{ item }}
                </view>
              </view>
            </picker-view-column>
          </picker-view>
        </view> -->

        <!-- 报考类型 -->
        <!-- <view class="report">
          <picker-view
            :value="report_1"
            class="picker-view"
            @change="
              (e) => {
                bindChange(e, 'report_1');
              }
            "
          >
            <picker-view-column>
              <view
                class="item"
                v-for="(item, index) in columns_1"
                :key="index"
              >
                <view :class="[index == report_1[0] ? 'active' : '']">
                  {{ item }}
                </view>
              </view>
            </picker-view-column>
          </picker-view>
          <view class="line"></view>
          <picker-view
            :value="report_2"
            class="picker-view"
            @change="
              (e) => {
                bindChange(e, 'report_2');
              }
            "
          >
            <picker-view-column>
              <view
                class="item"
                v-for="(item, index) in columns_2"
                :key="index"
              >
                <view :class="[index == report_2[0] ? 'active' : '']">
                  {{ item }}
                </view>
              </view>
            </picker-view-column>
          </picker-view>
        </view> -->

        <!-- 选择学校 -->
        <view class="school">
          <view class="school_title">
            <view class="left">
              <uv-icon name="map"></uv-icon>
              <view class="_in">邯郸理工学校</view>
            </view>
            <view class="right">
              <input placeholder="输入学校" class="right_inp" />
              <uv-icon name="search" size="20"></uv-icon>
            </view>
          </view>
          <view style="padding: 0px 40px">
            <picker-view
              :value="report_3"
              class="picker-view"
              @change="
                (e) => {
                  bindChange(e, 'report_3');
                }
              "
            >
              <picker-view-column>
                <view
                  class="item"
                  v-for="(item, index) in columns_3"
                  :key="index"
                >
                  <view :class="[index == report_3[0] ? 'active' : '']">
                    {{ item }}
                  </view>
                </view>
              </picker-view-column>
            </picker-view>
          </view>
        </view>
      </view>
    </uv-popup>
  </view>
</template>

<script setup>
import { ref } from "vue";
const popup = ref();
let candidateType = ref([0]);
let report_1 = ref([0]);
let report_2 = ref([0]);
let report_3 = ref([0]);
const columns = ref(["应届普高生", "中职生", "社会考生(往届)"]);
const columns_1 = ref(["高职单招-统考"]);
const columns_2 = ref(["考试十类", "考试九类", "考试八类(往届)"]);
const columns_3 = ref(["邯郸市职教中心", "邯郸市第二职业中学", "邯郸理工学校"]);

const open = () => {
  popup.value.open();
};

const bindChange = (e, type) => {
  type = e.detail.value;
};
</script>

<style lang="scss" scoped>
.title {
  margin-top: 38px;
  display: flex;
  align-items: center;
  padding-left: 15px;
  font-size: 26px;
  font-weight: 600;
  color: #3d3d3d;

  .img {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    border: 1px solid #1cd1de;
    margin-left: 18px;
  }
}
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

.list {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 31px;
  .item {
    width: 345px;
    padding: 0px 25px 0px 15px;
    border-radius: 14px;
    background: #ffffff;
    box-shadow: 0px 4px 8px 0px rgba(184, 216, 235, 0.2);
    .arrs {
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 1px solid #f0f0f0;
      padding: 12px 0px;
      ._left {
        //
        font-size: 14px;
        color: #6b7280;
      }
      ._right {
        display: flex;
        align-items: center;
        color: #9ca3af;
        font-size: 14px;
        .year {
          width: 64px;
          height: 24px;
          border-radius: 8px;
          background: #d2f6f8;
          line-height: 24px;
          text-align: center;
          margin-right: 10px;
        }
        ._t {
          padding-right: 10px;
        }
      }
    }
  }
}

.popBottom {
  background: #f8f8f8;
  padding: 0px 15px;
  ._title {
    padding: 0px 5px;
    height: 58px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    .cancel {
      color: #9ca3af;
      font-size: 14px;
    }
    .type {
      color: #1d2129;
      font-size: 16px;
      font-weight: 600;
    }
    .save {
      color: #1cd1de;
      font-size: 14px;
    }
  }

  .total {
    height: 208px;
    background: #ffffff;
    padding: 15px 20px;
    border-radius: 8px;
    .h11 {
      font-size: 14px;
      font-weight: 500;
      color: #3d3d3d;
    }
    .h55 {
      font-size: 12px;
      color: #9ca3af;
      padding-top: 2px;
    }
    .inpNum {
      margin-top: 20px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      .line {
        width: 15px;
        height: 1px;
        background: #d8d8d8;
      }
      .inp {
        width: 126px;
        height: 40px;
        border-radius: 8px;
        background: #f0f0f0;
        display: flex;
        align-items: center;
        justify-content: center;
      }
      .center-input {
        text-align: center !important;
        font-size: 12px;
        color: #6b7280;
      }
    }
  }

  .province {
    border-radius: 8px;
    background: #ffffff;
    ._title_1 {
      height: 51px;
      padding: 0px 7px;
      display: flex;
      align-items: center;
      border-bottom: 1px solid #f0f0f0;
      ._in {
        font-size: 14px;
        font-weight: 500;
        color: #1d2129;
        margin: 0px 11px;
      }
      .city {
        // width: 76px;
        height: 36px;
        background: #e8fafb;
        color: #1cd1de;
        font-size: 12px;
        line-height: 36px;
        text-align: center;
        border-radius: 8px;
        padding: 0px 20px;
      }
    }
    .other {
      font-size: 12px;
      color: #9ca3af;
      padding: 5px 15px 13px 15px;
    }
    ._scroll {
      width: 100%;
      height: 100%;
      ._scroll_item {
        display: inline-block;
        width: 20%;
        height: 36px;
        line-height: 36px;
        text-align: center;
        background: #f5f5f5;
        border-radius: 8px;
        color: #6b7280;
        font-size: 12px;
        margin: 0px 0px 8px 14px;
        text-overflow: ellipsis;
        overflow: hidden;
        word-break: break-all;
        white-space: nowrap;
      }
    }
  }

  .picker-view-box {
    border-radius: 8px;
    overflow: hidden;
    padding: 0px 40px;
    background: #ffffff;
    padding-bottom: 20px;
  }

  .report {
    height: 208px;
    border-radius: 8px;
    background: #ffffff;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0px 40px;
    .line {
      width: 1px;
      height: 20px;
      background: #1cd1de;
      margin: 0px 12px;
    }
  }
}
.picker-view {
  width: 100%;
  height: 180px;
  .item {
    line-height: 40px;
    text-align: center;
    color: #6b7280;
    font-size: 14px;
    font-weight: 350;
  }
  .active {
    font-size: 14px;
    font-weight: normal;
    color: #1cd1de;
  }
}

.school {
  height: 272px;
  border-radius: 8px;
  background: #ffffff;
  .school_title {
    height: 49px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0px 9px;
    border-bottom: 1px solid #f0f0f0;
    .left {
      display: flex;
      align-items: center;
      ._in {
        font-size: 12px;
        font-weight: 350;
        color: #1cd1de;
        padding-left: 6px;
      }
    }
    .right {
      display: flex;
      align-items: center;
      .right_inp {
        text-align: right;
        font-size: 14px;
        font-weight: 350;
        color: #9ca3af;
      }
    }
  }
}
</style>
