<template>
  <view>
    <customizeBar navBackgroundColor="#FFFFFF">
      <view class="pageTitle">
        <view class="_right">
          <view class="h4">高职单招</view>
          <view class="category">考试十类</view>
          <uv-icon name="arrow-down" size="18px" color="#1d2129"></uv-icon>
        </view>
        <view class="_left">
          <uv-icon name="map" size="18px" color="#1296DB"></uv-icon>
          <view class="city">考试十类</view>
        </view>
      </view>
    </customizeBar>

    <view class="pageContent">
      <view class="nav">
        <view class="navCenter">
          <view class="nav_item">
            <view class="icon">
              <image class="img" src="/static/pageImg/gerendangwen.png"></image>
            </view>
            <view class="text">个人档案</view>
          </view>
        </view>
        <view class="navCenter">
          <view class="nav_item">
            <view class="icon">
              <image
                class="img1"
                src="/static/pageImg/zhishidianlianxi.png"
              ></image>
            </view>
            <view class="text">知识点练习</view>
          </view>
        </view>
        <view class="navCenter">
          <view class="nav_item">
            <view class="icon">
              <image
                class="img2"
                src="/static/pageImg/zhinengsouti.png"
              ></image>
            </view>
            <view class="text">智能搜题</view>
          </view>
        </view>
        <view class="navCenter">
          <view class="nav_item">
            <view class="icon">
              <image class="img3" src="/static/pageImg/jiucuoti.png"></image>
            </view>
            <view class="text">错题本</view>
          </view>
        </view>
      </view>

      <view class="broadcast">
        <view class="rightView">
          <view class="z_c">未完成智能自测</view>
          <view class="f_a">解锁评级 立即获取专属提分方案</view>
          <view class="dengji">
            <image src="/static/pageImg/dengji_a.png"></image>
          </view>
          <image src="/static/pageImg/right_jt.png" class="right_jt"></image>
        </view>
      </view>

      <view class="vipBox">
        <view class="vip_title">
          <image
            class="weihuakevip"
            src="/static/pageImg/weihuakevip.png"
          ></image>
          <image
            class="zhuanyekevip"
            src="/static/pageImg/zhuanyekevip.png"
          ></image>
          <image class="svip" src="/static/pageImg/svip.png"></image>
        </view>
        <view class="lookVideo">
          <swiper class="swiper">
            <swiper-item>
              <view class="swiper_video">
                <view class="arrts">
                  解锁所有文化课知识题库
                  <image
                    src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimage109.360doc.com%2FDownloadImg%2F2021%2F04%2F2706%2F220904155_3_20210427065803991&refer=http%3A%2F%2Fimage109.360doc.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1757467030&t=47124e7652b45f9e7842714178da5c8f"
                    class="bg"
                  ></image>
                  <image class="jiantou"></image>
                </view>
                <view class="arrts">
                  解锁所有文化课视频课程
                  <image
                    src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimage109.360doc.com%2FDownloadImg%2F2021%2F04%2F2706%2F220904155_3_20210427065803991&refer=http%3A%2F%2Fimage109.360doc.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1757467030&t=47124e7652b45f9e7842714178da5c8f"
                    class="bg"
                  ></image>
                  <image class="jiantou"></image>
                </view>
              </view>
            </swiper-item>
            <swiper-item>
              <view class="swiper-item uni-bg-green">B</view>
            </swiper-item>
            <swiper-item>
              <view class="swiper-item uni-bg-blue">C</view>
            </swiper-item>
          </swiper>
        </view>
      </view>

      <view class="task">
        <view class="task_t">
          <view class="_l">作业&考试</view>
          <view class="_r">查看全部</view>
        </view>

        <view class="item">
          <view class="item_t">
            <view class="kaoshi">考试</view>
            <view class="time">剩余15h</view>
          </view>
          <view class="item_y">
            <view class="ceyan">数学5月28日作业测验</view>
            <view class="progress">
              <uv-line-progress
                :percentage="30"
                :showText="false"
              ></uv-line-progress>
              <text style="padding-left: 16rpx">80%</text>
            </view>
          </view>
          <view class="type">已完成</view>
          <image class="jiantou" src="/static/pageImg/right_jt.png"></image>
        </view>
      </view>

      <view class="task">
        <view class="task_t">
          <view class="_l">提分策略</view>
          <view class="_r"></view>
        </view>
      </view>
    </view>
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
    .city {
      font-size: 24rpx;
      font-weight: 350;
      color: #3d3d3d;
      padding-left: 10rpx;
    }
  }
}

.pageContent {
  padding: 30rpx;
  display: flex;
  flex-direction: column;
  .nav {
    width: 100%;
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    background: #ffffff;
    border-radius: 18rpx;
    .navCenter {
      width: 25%;
      display: flex;
      align-items: center;
      justify-content: center;
      .nav_item {
        width: 120rpx;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 20rpx 30rpx;
        .icon {
          width: 104rpx;
          height: 104rpx;
          background: #ffffff;
          border-radius: 50%;
          display: flex;
          align-items: center;
          justify-content: center;
          .img {
            width: 70rpx;
            height: 70rpx;
          }
          .img1 {
            width: 76rpx;
            height: 76rpx;
          }
          .img2 {
            width: 66rpx;
            height: 60rpx;
          }
          .img3 {
            width: 82rpx;
            height: 82rpx;
          }
        }
        .text {
          font-size: 24rpx;
          color: #3d3d3d;
          padding-top: 24rpx;
          width: 160rpx;
          text-align: center;
        }
      }
    }
  }

  .broadcast {
    margin-top: 34rpx;
    display: flex;
    flex-direction: row-reverse;
    .rightView {
      width: 652rpx;
      height: 164rpx;
      border-radius: 100rpx;
      background: linear-gradient(353deg, #7477ff 25%, #a1ebf0 93%);
      position: relative;
      display: flex;
      flex-direction: column;
      justify-content: center; /* 垂直居中 */
      align-items: flex-start; /* 水平靠左 */
      .z_c {
        font-size: 30rpx;
        font-weight: bold;
        color: #ffffff;
        padding-left: 90rpx;
        font-style: italic;
      }
      .f_a {
        font-size: 20rpx;
        font-weight: bold;
        color: #ffffff;
        padding: 4rpx 0rpx;
        padding-left: 90rpx;
        font-style: italic;
      }
      .dengji {
        padding-left: 90rpx;
        image {
          width: 40rpx;
          height: 40rpx;
        }
      }
      .right_jt {
        position: absolute;
        right: 24rpx;
        bottom: 50rpx;
        width: 48rpx;
        height: 48rpx;
      }
    }
  }

  .vipBox {
    display: flex;
    flex-direction: column;
    margin-top: 42rpx;
    .vip_title {
      height: 46rpx;
      position: relative;
      .weihuakevip {
        width: 176rpx;
        height: 46rpx;
        position: absolute;
        left: 0rpx;
        top: 0rpx;
      }
      .zhuanyekevip {
        width: 218rpx;
        height: 46rpx;
        position: absolute;
        left: 128rpx;
        top: 0rpx;
      }
      .svip {
        position: absolute;
        left: 298rpx;
        top: 0rpx;
        width: 218rpx;
        height: 46rpx;
      }
    }
    .lookVideo {
      border-radius: 0rpx 28rpx 28rpx 28rpx;
      background: #ffffff;
      overflow: hidden;
      .swiper {
        height: 230rpx;
        .swiper_video {
          width: 100%;
          display: flex;
          align-items: center;
          justify-content: space-around;
          margin-top: 40rpx;
          .arrts {
            width: 306rpx;
            height: 146rpx;
            line-height: 146rpx;
            text-align: center;
            border-radius: 22rpx;
            font-size: 24rpx;
            color: #3d3d3d;
            position: relative;
            overflow: hidden;
            .bg {
              position: absolute;
              left: 0rpx;
              top: 0rpx;
              width: 306rpx;
              height: 146rpx;
              z-index: -1;
            }
            .jiantou {
              position: absolute;
              right: 0rpx;
              bottom: 0rpx;
              width: 48rpx;
              height: 48rpx;
            }
          }
        }
      }
    }
  }

  .task {
    display: flex;
    flex-direction: column;
    margin-top: 14rpx;
    .task_t {
      display: flex;
      align-items: center;
      justify-content: space-between;
      ._l {
        font-size: 32rpx;
        color: #3d3d3d;
        font-weight: bold;
      }
      ._r {
        font-size: 24rpx;
        color: #6b7280;
      }
    }
    .item {
      display: flex;
      align-items: center;
      background: #ffffff;
      border-radius: 28rpx;
      height: 140rpx;
      margin-top: 10rpx;
      position: relative;
      .item_t {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-left: 15rpx;
        .kaoshi {
          width: 96rpx;
          height: 42rpx;
          line-height: 42rpx;
          text-align: center;
          background: linear-gradient(
            90deg,
            rgba(219, 209, 253, 0.78) 0%,
            #4cd7e8 99%
          );
          border-radius: 22rpx;
          font-size: 24rpx;
          color: #ffffff;
        }
        .time {
          font-size: 22rpx;
          color: #9ca3af;
          padding-top: 20rpx;
        }
      }
      .item_y {
        display: flex;
        flex-direction: column;
        align-items: center;
        align-items: flex-start; /* 水平靠左 */
        padding-left: 22rpx;
        .ceyan {
          font-size: 28rpx;
          color: #6b7280;
          padding-bottom: 20rpx;
        }
        .progress {
          display: flex;
          align-items: center;
          width: 400rpx;
          font-size: 24rpx;
          color: #9ca3af;
        }
      }
      .type {
        position: absolute;
        right: 0rpx;
        top: 0rpx;
        width: 122rpx;
        height: 46rpx;
        line-height: 46rpx;
        text-align: center;
        border-radius: 0rpx 28rpx 0rpx 28rpx;
        background: #ffe5cc;
        font-size: 22rpx;
        color: #ff8f1f;
      }
      .jiantou {
        position: absolute;
        right: 9rpx;
        bottom: 8rpx;
        width: 48rpx;
        height: 48rpx;
      }
    }
  }
}
</style>
