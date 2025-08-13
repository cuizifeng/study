<template>
  <view>
    <customizeBar navBackgroundColor="#FFFFFF">
      <view class="pageTitle">
        <view class="_right" @click="back">
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
    <view v-if="total > 0" class="overflow-y-auto">
      <view class="mt-8 top">
        <uv-subsection
          customStyle="height:76rpx;background-color: #FFFFFF;"
          fontSize="30rpx"
          activeColor="#3D5CFF"
          :list="subsectionList"
          mode="subsection"
          :current="subsectionCurrent"
          @change="modeChange"
          v-if="type == 1"
        ></uv-subsection>

        <view v-if="type == 2" class="p-10 fs-17 fw-600 text-center">
          {{ secondsToMS(countdown) }}
        </view>
      </view>
      <view class="px-15 mt-8 overflow-y-auto mb-130">
        <view class="flex flex-y-center">
          <uv-line-progress
            height="5"
            :showText="false"
            :percentage="percentage"
            activeColor="#3D5CFF"
            inactiveColor="#fff"
          ></uv-line-progress>
          <view class="text-blue-1 fs-16 fw-600 ml-15">
            {{ current + 1 }}
            <span class="fs-14 text-grey-4 fw-400">/{{ total }}</span>
          </view>
        </view>
        <view
          :class="aniClass"
          @touchstart="touchStart"
          @touchmove="touchMove"
          @touchend="touchEnd"
          style="min-height: calc(100vh - 140px)"
          class="overflow-y-scroll"
        >
          <view class="bg-white rounded-12 p-20 mt-8 animated-element">
            <view class="fw-600 fs-15">
              <text
                class="question-type text-blue-1 px-10 py-4 rounded-4 block fs-12"
              >
                {{ getStyleText(topic?.type) }}
              </text>
              {{ current + 1 }}. {{ topic?.topic }}
            </view>
            <image
              class="w-p-100 mt-20"
              mode="widthFix"
              v-if="topic?.image"
              :src="topic?.image"
            ></image>
            <!-- 单选 -->
            <view v-if="topic?.type == 'single'">
              <view
                class="flex mt-20 flex-y-center flex-x-space-between"
                :key="index"
                v-for="(item, index) in topic?.option"
                @click="onSingleAnswer(item.value)"
              >
                <view class="flex flex-y-center">
                  <text
                    class="w-30 mw-30 text-grey-5 border-grey-5 h-30 fs-14 fw-500 rounded-circle flex flex-center"
                    :class="getSingleClass(item.value, 1)"
                  >
                    {{ item.value }}
                  </text>
                  <text
                    class="text-grey-5 fs-14 ml-10"
                    :class="getSingleClass(item.value, 2)"
                  >
                    {{ item.label }}
                  </text>
                </view>
                <uv-icon
                  name="checkmark-circle-fill"
                  color="#2ae295"
                  size="20"
                  v-if="topic.status == true && topic.answer == item.value"
                ></uv-icon>
                <uv-icon
                  name="close-circle-fill"
                  color="#eb3b3b"
                  size="20"
                  v-if="
                    topic.status == true &&
                    topic.userAnswer == item.value &&
                    topic.answer != item.value
                  "
                ></uv-icon>
              </view>
            </view>
            <!-- 多选 -->
            <view v-if="topic?.type == 'multiple'">
              <view
                class="flex mt-20 flex-y-center flex-x-space-between"
                v-for="(item, index) in topic?.option"
                @click="onMultipleAnswer(item.value)"
                :key="index"
              >
                <view class="flex flex-y-center">
                  <view
                    class="w-16 h-16 flex flex-center box-sizing border-grey-1 rounded-4"
                    :class="getMultipleClass(item.value, 1)"
                  >
                    <view
                      class="w-10 h-10 rounded-2"
                      :class="getMultipleClass(item.value, 2)"
                    ></view>
                  </view>
                  <text
                    class="text-grey-5 fs-14 ml-10"
                    :class="getMultipleClass(item.value, 3)"
                  >
                    {{ item.value }} {{ item.label }}
                  </text>
                </view>

                <uv-icon
                  name="checkmark-circle-fill"
                  color="#2ae295"
                  size="20"
                  v-if="getIconStatus(item.value, true)"
                ></uv-icon>

                <uv-icon
                  name="close-circle-fill"
                  color="#eb3b3b"
                  size="20"
                  v-if="getIconStatus(item.value, false)"
                ></uv-icon>
              </view>
            </view>

            <view
              v-if="subsectionCurrent == 1 && topic?.type == 'blank'"
              class="p-12 bg-grey-6 rounded-8 mt-10 text-blue-1 border-blue-1"
            >
              <text class="fs-12 text-grey-3">{{ topic?.answer }}</text>
            </view>

            <view
              v-if="
                topic?.type == 'blank' &&
                subsectionCurrent == 0 &&
                !topic.status
              "
              class="p-12 bg-grey-6 rounded-8 mt-10"
              :class="{
                'text-red-1 border-red-1':
                  topic?.answer != topic?.userAnswer && topic?.status == true,
                'text-blue-1 border-blue-1': topic?.answer == topic?.userAnswer,
              }"
            >
              <input
                placeholder="请输入你的答案"
                v-model="blankAnswer"
                :disabled="topic?.status"
                placeholder-class="fs-12 text-grey-3"
              />
            </view>

            <view
              v-if="
                topic?.type == 'blank' && subsectionCurrent == 0 && topic.status
              "
              class="p-12 bg-grey-6 rounded-8 mt-10"
              :class="{
                'text-red-1 border-red-1':
                  topic?.answer != topic?.userAnswer && topic?.status == true,
                'text-blue-1 border-blue-1': topic?.answer == topic?.userAnswer,
              }"
            >
              <text class="fs-12 text-grey-3">{{ topic?.userAnswer }}</text>
            </view>
          </view>

          <view
            class="px-50 mt-27"
            v-if="topic?.type == 'multiple' && multipleAnswer.length > 0"
          >
            <view
              class="w-p-100 py-11 rounded-8 bg-blue-1 text-white fs-16 text-center"
              @click="submitAnswer()"
            >
              确认
            </view>
          </view>

          <view
            class="px-50 mt-27"
            v-if="
              subsectionCurrent == 0 && topic?.type == 'blank' && !topic?.status
            "
          >
            <view
              class="w-p-100 py-11 rounded-8 bg-blue-1 text-white fs-16 text-center"
              @click="submitBlank()"
            >
              确认
            </view>
          </view>

          <view v-if="topic?.status == true || subsectionCurrent == 1">
            <view class="bg-white rounded-12 p-10 mt-8">
              <view
                class="flex flex-x-space-between flex-y-center fw-600 mb-10"
              >
                <view class="flex flex-y-center">
                  <view
                    class="bg-blue-1 rounded-top-right-8 rounded-bottom-right-8 w-4 h-15"
                  ></view>
                  <text class="fs-17 ml-5">试题答案</text>
                </view>
                <text class="fs-15 text-blue-1" @click="openFeedback()">
                  纠错留言
                </text>
              </view>
              <text class="fs-14 text-grey-5">
                正确答案 {{ topic?.answer }}
              </text>
              <view class="fs-14 text-grey-5 flex flex-y-center mt-10">
                难度:
                <view class="flex">
                  <image
                    v-for="item in 5"
                    :key="item"
                    :src="
                      item <= topic?.difficulty
                        ? '/static/icon/star_s.png'
                        : '/static/icon/star.png'
                    "
                    class="w-15 h-15 ml-9"
                  ></image>
                </view>
              </view>
            </view>

            <view class="bg-white rounded-12 p-10 mt-8">
              <view class="flex flex-y-center mb-10">
                <view
                  class="bg-blue-1 rounded-top-right-8 rounded-bottom-right-8 w-4 h-15"
                ></view>
                <text class="fs-17 fw-600 ml-5">答案解析</text>
              </view>
              <text class="fs-14 text-grey-5">{{ topic?.analysis }}</text>
            </view>
          </view>
        </view>
      </view>
    </view>

    <view
      class="bg-white position-fixed bottom-0 box-sizing left-0 right-0 fw-600 pb-safe-area"
      v-if="total > 0"
    >
      <view class="px-15 py-8 flex flex-y-center">
        <view class="flex flex-x-space-between ml-5 w-p-30">
          <view
            class="flex flex-column flex-center"
            @click="collectTopic()"
            v-if="type == 1"
          >
            <image
              src="/static/pageImg/star_sc.png"
              v-if="topic?.collect_id != null"
              class="w-24 h-24"
            ></image>
            <image
              src="/static/pageImg/star.png"
              v-else
              class="w-24 h-24"
            ></image>
            <view class="fs-12 text-grey-3 mt-6">
              {{ topic?.collect_id != null ? "取消收藏" : "立即收藏" }}
            </view>
          </view>
          <view
            class="flex flex-column flex-center"
            @click="openTips()"
            v-if="type == 2"
          >
            <image src="/static/pageImg/jj.png" class="w-24 h-24"></image>
            <view class="fs-12 text-grey-3 mt-6">交卷</view>
          </view>
          <view
            class="flex flex-column flex-center ml-16"
            @click.stop="openPopup()"
          >
            <image src="/static/pageImg/jx.png" class="w-24 h-24"></image>
            <view class="fs-12 text-grey-3 mt-6">答题卡</view>
          </view>
        </view>
        <view
          class="py-10 ml-30 px-25 border-blue-1 text-blue-1 rounded-4 fs-15 block"
          @click.stop="changeTopic(current - 1)"
        >
          上一题
        </view>
        <view
          class="py-10 ml-10 px-25 bg-blue-1 text-white rounded-4 fs-15 block"
          @click.stop="changeTopic(current + 1)"
        >
          下一题
        </view>
      </view>
    </view>

    <uv-popup ref="popup" round="16">
      <view class="px-20 popup">
        <view class="text-center py-20">
          <text class="fs-18 fw-600">答题卡</text>
        </view>
        <view class="flex">
          <view class="flex flex-y-center">
            <view class="rounded-circle w-7 h-7 bg-grey-1"></view>
            <view class="fs-14 ml-4">未答</view>
          </view>
          <view class="flex flex-y-center ml-20">
            <view class="rounded-circle w-7 h-7 bg-green-1"></view>
            <view class="fs-14 ml-4">答对</view>
          </view>
          <view class="flex flex-y-center ml-20">
            <view class="rounded-circle w-7 h-7 bg-red-1"></view>
            <view class="fs-14 ml-4">答错</view>
          </view>
        </view>
        <view class="dtk-box pb-20">
          <view
            v-for="(item, index) in topicList"
            :key="index"
            @click="onChange(index)"
            class="border-grey-1 w-40 h-40 rounded-circle text-grey-1 flex flex-center fs-17 mt-20 ml-4"
            :class="{
              'border-green-1 text-green-1': item.answer == item.userAnswer,
              'border-red-1 text-red-1':
                item.status == true && item.answer != item.userAnswer,
            }"
          >
            {{ index + 1 }}
          </view>
        </view>
      </view>
    </uv-popup>

    <uv-popup ref="popupFeedback" round="8" custom-style="width: 80%">
      <view class="p-20 text-center">
        <text class="fw-600 fs-16">错题反馈</text>
        <view
          class="p-10 mt-16 rounded-6 text-left"
          style="background-color: #f5f5f5"
        >
          <textarea
            placeholder="请输入你的建议"
            v-model="content"
            style="width: 100%; height: 200rpx"
          ></textarea>
        </view>
        <view class="px-10 mt-20 flex flex-x-space-between">
          <view
            class="py-6 px-35 border-grey-1 text-grey-1 rounded-30 fs-15 block"
            @click="closeFeedback()"
          >
            取消
          </view>
          <view
            class="py-6 px-35 border-blue-1 text-blue-1 rounded-30 fs-15 block"
            @click="submitFeedback()"
          >
            提交
          </view>
        </view>
      </view>
    </uv-popup>

    <uv-popup
      ref="popupTips"
      round="12"
      :closeOnClickOverlay="false"
      :safeAreaInsetBottom="false"
    >
      <view class="popup bg-white p-16 flex flex-center flex-column rounded-5">
        <y-circle
          ref="ani"
          :size="100"
          :percent="100 - (completed / total) * 100"
          circleColor="#f24551"
          :animation="true"
          :animationSpeed="15"
          :direction="180"
        >
          <template #content>
            <view class="flex flex-column flex-y-center">
              <view class="fs-14">未做题</view>
              <view class="mt-3">{{ total - completed }}题</view>
            </view>
          </template>
        </y-circle>
        <view class="fs-14 text-grey-1 mt-5">
          剩余时间 {{ secondsToMS(countdown) }}
        </view>
        <view
          class="flex box-sizing vw-60 flex-x-space-between mt-10 text-center"
        >
          <view
            v-if="completed < total && countdown != 0"
            class="py-10 box-sizing border-blue-1 text-blue-1 rounded-30 fs-15 block vw-25"
            @click="resume()"
          >
            继续
          </view>
          <view
            :class="completed < total && countdown != 0 ? 'vw-25' : 'vw-60'"
            class="py-10 box-sizing bg-blue-1 text-white rounded-30 fs-15 block"
            @click="achievement()"
          >
            交卷
          </view>
        </view>
      </view>
    </uv-popup>

    <y-loading v-if="statusShow"></y-loading>
    <y-empty v-if="empty"></y-empty>
  </view>
</template>

<script setup>
/*******************导入**********************/
import { reactive, ref, computed, nextTick } from "vue";
import { onLoad, onUnload, onHide } from "@dcloudio/uni-app";
import testJson from "./a.json";
//import { $http, $page, $tool, useStorage } from "@/utils/index";
/*******************导入**********************/

/*******************变量**********************/

const height = uni.getSystemInfoSync().safeAreaInsets.bottom;
//考试信息
const testPaper = ref({
  test_paper_id: 0,
  correct_ids: [],
  wrong_ids: [],
  time: 0,
  topic_num: 0,
});

//错误 正确信息
const wrongIds = ref([]);
const correctIds = ref([]);
const weekWrongIds = ref([]);
const weekCorrectIds = ref([]);
const monthWrongIds = ref([]);
const monthCorrectIds = ref([]);

//动画
const ani = ref(null);
//交卷提示
const popupTips = ref();
//已作答数量
const completed = ref(0);
//定时器
const time = ref();
//考试倒计时
const countdown = ref(60);
//类型 1刷题模式 2考试模式
const type = ref(1);
//加载动画
const statusShow = ref(false);
//模式
const subsectionCurrent = ref(0);
const subsectionList = reactive(["答题模式", "背题模式"]);
//题目集合
const topicList = ref();
//当前题目
const topic = ref();
//总数量
const total = ref(0);
//当前条数
const current = ref(0);
//填空答案
const blankAnswer = ref();
//多选答案
const multipleAnswer = ref([]);
//多选题提交状态
const submitStatus = ref(false);
//答题卡弹窗
const popup = ref();
//动画效果
const aniClass = ref();
//触摸相关
const startX = ref();
const endX = ref();
//反馈弹窗
const popupFeedback = ref();
//反馈文字
const content = ref();
//缺省
const empty = ref(false);
//条件
const queryForm = ref({
  type: 0,
  category_id: 0,
  rand: 0,
  search_id: 0,
  classification_id: 0,
});
/*******************变量**********************/

/*******************计算属性**********************/

//进度 百分比
const percentage = computed(() => {
  return ((current.value + 1) / total.value) * 100;
});
/*******************计算属性**********************/

onLoad((option) => {
  if (option.testPaperId) {
    getWrongList(option.testPaperId);
    return;
  }
  let id = "";
  //  useStorage().get("CATEGORY");
  if (id) {
    queryForm.value.classification_id = id;
  }
  if (option.search_id) {
    queryForm.value.search_id = option.search_id;
  }
  if (option.type) {
    queryForm.value.type = option.type;
  }
  if (option.category_id) {
    queryForm.value.category_id = option.category_id;
  }
  if (option.rand) {
    queryForm.value.rand = 1;
  }
  if (option.id || true) {
    type.value = option.type;
    testPaper.value.test_paper_id = option.id;
    getTestPaperList();
  } else {
    // getList();
  }
});
onUnload(() => {
  save();
});

onHide(() => {
  // save();
});

/*******************考试相关方法**********************/
const save = () => {
  if (type.value != 2) {
    $http.post("Record/record", {
      wrong_ids: wrongIds.value,
      correct_ids: correctIds.value,
      week_wrong_ids: weekWrongIds.value,
      week_correct_ids: weekCorrectIds.value,
      month_wrong_ids: monthWrongIds.value,
      month_correct_ids: monthCorrectIds.value,
      classification_id: queryForm.value.classification_id,
    });
  }
};
//获取考试题目
const getTestPaperList = () => {
  console.log("arrs", testJson);
  // $http
  //   .get("TestPaper/getTestPaperList", { id: testPaper.value.test_paper_id })
  //   .then((res) => {
  topicList.value = testJson.data.list;
  total.value = testJson.data.info.number;
  countdown.value = testJson.data.info.time * 60;
  testPaper.value.time = testJson.data.info.time * 60;
  testPaper.value.topic_num = testJson.data.info.number;
  countDownTime();
  changeTopic(0);
  // });
};
//倒计时
const countDownTime = () => {
  time.value = setInterval(() => {
    countdown.value--;
    // console.log(countdown.value);
    if (countdown.value == 0) {
      openTips();
    }
  }, 1000);
};

//交卷
const achievement = () => {
  testPaper.value.time = testPaper.value.time - countdown.value;
  $http.post("TestPaper/achievement", testPaper.value).then((res) => {
    $tool.toast("提交成功");
    setTimeout(() => {
      $page.redirect("/pages/testPaper/result?id=" + res.data.id);
    }, 500);
  });
};

//继续答题
const resume = () => {
  countDownTime();
  popupTips.value.close();
};
//弹窗 暂停倒计时
const openTips = () => {
  clearInterval(time.value);
  popupTips.value.open("center");
  nextTick(() => {
    console.log(ani.value);
    ani.value.loadAnimation();
  });
};

//友好时间显示
const secondsToMS = (seconds) => {
  const m = Math.floor(seconds / 60);
  const s = seconds % 60;
  return `${padTo2Digits(m)}:${padTo2Digits(s)}`;
};
const padTo2Digits = (num) => {
  return num.toString().padStart(2, "0");
};
/*******************考试相关方法**********************/

//获取错误记录
const getWrongList = (id) => {
  $http.get("/TestPaper/getWrongRecord", { id: id }).then((res) => {
    topicList.value = res.data;
    total.value = res.data.length;
    if (total.value == 0) {
      empty.value = true;
      return;
    }
    changeTopic(0);
  });
};

//获取往期答题
const getRecord = () => {
  $http
    .get("record/getRecord", {
      classification_id: queryForm.value.classification_id,
    })
    .then((res) => {
      wrongIds.value = res.data.record.wrong_ids || [];
      correctIds.value = res.data.record.correct_ids || [];
      weekWrongIds.value = res.data.week.wrong_ids || [];
      weekCorrectIds.value = res.data.week.correct_ids || [];
      monthWrongIds.value = res.data.month.wrong_ids || [];
      monthCorrectIds.value = res.data.month.correct_ids || [];
    });
};

//获取列表
const getList = () => {
  statusShow.value = true;
  $http
    .get("Topic/getList", queryForm.value)
    .then((res) => {
      topicList.value = res.data.data;
      total.value = res.data.total;
      if (total.value == 0) {
        empty.value = true;
        return;
      }
      changeTopic(0);
    })
    .finally(() => {
      statusShow.value = false;
    });
};
//获取类型
const getStyleText = (e) => {
  if (e == "single") {
    return "单选题";
  }
  if (e == "multiple") {
    return "多选题";
  }
  if (e == "blank") {
    return "填空题";
  }
};

const updateTopic = (userAnswer) => {
  const tempTopic = topic.value;
  if (tempTopic.status) {
    return;
  }
  tempTopic.status = true;
  tempTopic.userAnswer = userAnswer;
  topic.value = tempTopic;
  topicList.value[current.value] = tempTopic;
  completed.value++;
  if (tempTopic.answer == userAnswer) {
    setTimeout(() => {
      changeTopic(current.value + 1);
    }, 300);
    testPaper.value.correct_ids.push(tempTopic.id);
    record(tempTopic.id, true);
  } else {
    testPaper.value.wrong_ids.push(tempTopic.id);
    record(tempTopic.id, false);
  }
};

const record = (id, res) => {
  const updateIds = (id, listAdd, listRemove) => {
    const addIndex = listAdd.value.indexOf(id);
    const removeIndex = listRemove.value.indexOf(id);

    if (addIndex === -1) {
      listAdd.value.push(id);
    }
    if (removeIndex !== -1) {
      listRemove.value.splice(removeIndex, 1);
    }
  };

  const removeIds = (id, listAdd, listRemove) => {
    const addIndex = listAdd.value.indexOf(id);
    const removeIndex = listRemove.value.indexOf(id);

    if (addIndex !== -1) {
      listAdd.value.splice(addIndex, 1);
    }
    if (removeIndex === -1) {
      listRemove.value.push(id);
    }
  };

  if (res === true) {
    updateIds(id, correctIds, wrongIds);
    updateIds(id, weekCorrectIds, weekWrongIds);
    updateIds(id, monthCorrectIds, monthWrongIds);
  } else {
    removeIds(id, correctIds, wrongIds);
    removeIds(id, weekCorrectIds, weekWrongIds);
    removeIds(id, monthCorrectIds, monthWrongIds);
  }
};

//选择答案 单选
const onSingleAnswer = (e) => {
  if (subsectionCurrent.value == 1) {
    return;
  }
  updateTopic(e);
};

//多选提交答案
const submitAnswer = () => {
  const answer1 = multipleAnswer.value.join(",");
  updateTopic(answer1);
  multipleAnswer.value = [];
};
//填空题答案
const submitBlank = () => {
  if (blankAnswer.value == "") {
    $tool.toast("请填写答案");
    return;
  }
  updateTopic(blankAnswer.value);
};

//选择 多选
const onMultipleAnswer = (e) => {
  if (topic.value.status || subsectionCurrent.value == 1) {
    return;
  }
  const index = multipleAnswer.value.indexOf(e);
  if (index === -1) {
    multipleAnswer.value.push(e);
  } else {
    multipleAnswer.value.splice(index, 1);
  }
  multipleAnswer.value.sort();
};

//切换题目
const onChange = (e) => {
  changeTopic(e);
  popup.value.close();
};

const changeTopic = (index) => {
  if (completed.value == total.value && type.value == 2) {
    openTips();
    return;
  }
  if (!topicList.value[index]) {
    $tool.toast("没有更多了");
    return;
  }

  blankAnswer.value = "";
  topic.value = topicList.value[index];
  topic.value.answer = topic.value.answer.trim();
  multipleAnswer.value = [];
  aniClass.value = index - current.value > 0 ? "animated-l" : "animated-r";
  current.value = index;
  setTimeout(() => {
    aniClass.value = "";
  }, 300);
};

//模式切换
const modeChange = (e) => {
  subsectionCurrent.value = e;
};

//单选样式
const getSingleClass = (item, type) => {
  const tempTopic = topic.value;
  if (!tempTopic.status && subsectionCurrent.value == 0) {
    return;
  }
  const isCorrectAnswer = item === tempTopic.answer;
  const isUserSelectedWrongAnswer =
    tempTopic.userAnswer === item && tempTopic.userAnswer !== tempTopic.answer;
  const getClass = (correctClass, wrongClass) => {
    if (isCorrectAnswer) {
      return correctClass;
    }
    if (isUserSelectedWrongAnswer) {
      return wrongClass;
    }
  };
  switch (type) {
    case 1:
      return getClass(
        "text-blue-1 bg-blue-1 border-blue-1 text-white",
        "text-red-1 border-red-1"
      );
    case 2:
      return getClass("text-blue-1", "text-red-1");
    default:
      return;
  }
};

//多选样式
const getMultipleClass = (e, type) => {
  const tempTopic = topic.value;
  let isUserSelected = null;
  let isCorrectAnswer = null;
  if (tempTopic.status == true) {
    isUserSelected = tempTopic.userAnswer.split(",").includes(e);
  }
  isCorrectAnswer = tempTopic.answer.split(",").includes(e);
  const commonLogic = (correctClass, incorrectClass) => {
    if (subsectionCurrent.value == 1 && isCorrectAnswer) {
      return correctClass;
    }

    if (tempTopic.status === true) {
      if (isCorrectAnswer && isUserSelected) {
        return correctClass;
      }

      if (isCorrectAnswer && !isUserSelected) {
        if (type != 2) {
          return incorrectClass;
        }
      }

      if (!isCorrectAnswer && isUserSelected) {
        return incorrectClass;
      }
    }

    if (multipleAnswer.value.includes(e)) {
      return correctClass;
    }
  };

  switch (type) {
    case 1:
      return commonLogic("border-blue-1", "border-red-1");
    case 2:
      return commonLogic("bg-blue-1", "bg-red-1");
    case 3:
      return commonLogic("text-blue-1", "text-red-1");
    default:
      return "";
  }
};

//图标状态
const getIconStatus = (e, status) => {
  const tempTopic = topic.value;
  if (!tempTopic.status) {
    return;
  }

  const isCorrectAnswer = tempTopic.answer.includes(e);
  const isUserSelected = tempTopic.userAnswer.includes(e);

  if (status === true && isCorrectAnswer) {
    return true;
  }

  if (status === false && isUserSelected && !isCorrectAnswer) {
    return true;
  }
};

//屏幕触摸开始
const touchStart = (e) => {
  startX.value = e.touches[0].clientX;
  endX.value = e.touches[0].clientX;
};
//移动
const touchMove = (e) => {
  endX.value = e.touches[0].clientX;
};
//结束
const touchEnd = () => {
  let number = startX.value - endX.value;
  if (number > 60) {
    changeTopic(current.value + 1);
  }
  if (number < -60) {
    changeTopic(current.value - 1);
  }
  startX.value = 0;
  endX.value = 0;
};

//收藏/取消收藏题目
const collectTopic = () => {
  $http.post("collect/Collect", { id: topic.value.id }).then((res) => {
    $tool.toast(res.msg);
    if (topic.value.collect_id) {
      topic.value.collect_id = null;
    } else {
      topic.value.collect_id = topic.value.id;
    }
  });
};
//提交
const submitFeedback = () => {
  $http
    .post("Topic/topicErrRecord", {
      id: topic.value.id,
      content: content.value,
    })
    .then((res) => {
      $tool.toast(res.msg);
      closeFeedback();
    });
};
const back = () => {
  // if (type.value != 2) {
  //   $page.back();
  //   return;
  // }
  openTips();
};

//答题卡打开
const openPopup = () => {
  popup.value.open("bottom");
};
//关闭
const closeFeedback = () => {
  popupFeedback.value.close();
};
//纠错弹窗
const openFeedback = () => {
  content.value = "";
  popupFeedback.value.open("center");
};
</script>

<style scoped lang="scss">
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
.top {
  padding: 0rpx 128rpx 0rpx 128rpx;
}

.question-type {
  background: rgba(61, 92, 255, 0.1);
}

.dtk-box {
  display: grid;
  grid-template-columns: repeat(6, 16.666%);
}

.popup {
  max-height: 50vh;
  overflow-y: auto;
}

.mb-130 {
  margin-bottom: 260rpx;
}

/* 定义动画 */
@keyframes moveRight {
  from {
    transform: translateX(-100%);
  }

  to {
    transform: translateX(0);
  }
}

/* 定义动画 */
@keyframes moveLeft {
  from {
    transform: translateX(100%);
  }

  to {
    transform: translateX(0);
  }
}

/* 应用动画到元素 */
.animated-r {
  animation: moveRight 0.3s ease forwards;
}

.animated-l {
  animation: moveLeft 0.3s ease forwards;
}

.mw-30 {
  min-width: 60rpx;
}
</style>
