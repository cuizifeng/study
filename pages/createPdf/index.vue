<template>
  <div
    class="containerBox"
    :style="{
      transform: `scale(${scaleRatio})`,
      transformOrigin: 'left top',
    }"
  >
    <div class="pdfDom" style="width: 595px; height: 842px; overflow: hidden">
      <view class="container" style="width: 100%; height: 100%">
        <view class="header">
          <text class="title">B</text>
        </view>

        <view class="content">
          <view class="subtitle">
            <text>通过大数据模型引擎分析</text>
          </view>

          <view class="report-card">
            <text class="report-title">自测分析报告</text>
            <text class="report-title">和学业提案</text>

            <view class="info-grid">
              <view class="info-row">
                <text class="info-label">学生</text>
                <text class="info-value">中职生</text>
              </view>
              <view class="info-row">
                <text class="info-label">地区</text>
                <text class="info-value">河北·邯郸</text>
              </view>
              <view class="info-row">
                <text class="info-label">时间</text>
                <text class="info-value">2025/08/14</text>
              </view>
              <view class="info-row">
                <text class="info-label">科目</text>
                <text class="info-value">语文</text>
              </view>
            </view>
          </view>

          <view class="footer">
            <text>海量数据·分析稳定·捕捉教育</text>
          </view>
        </view>
        <button @click="btnClick">12356</button>
      </view>
    </div>

    <div class="pdfDom">测试数据2</div>
    <div class="pdfDom">测试数据3</div>
  </div>
</template>

<script setup>
import { computed } from "vue";
// import html2Canvas from "html2canvas";
import JsPDF from "jspdf";

const scaleRatio = computed(() => {
  return uni.getSystemInfoSync().windowWidth / 595;
});

const btnClick = () => {
  htmlToPdf("pdfDom", "个人报告");
};
const htmlToPdf = (name, title) => {
  return;
  const element = document.querySelectorAll(`.${name}`);
  let count = 0;
  const PDF = new JsPDF("", "pt", "a4");
  const pageArr = [];
  // 设置A4纸尺寸（595.28×841.89 pt）
  const a4Width = 595.28;
  const a4Height = 841.89;
  const opts = {
    scale: 3, // 清晰度与性能平衡
    useCORS: true,
    allowTaint: false,
    logging: false,
    width: a4Width, // 固定宽度
    height: a4Height, // 固定高度
    windowWidth: a4Width,
    windowHeight: a4Height,
    scrollX: 0,
    scrollY: 0,
  };
  for (const index in Array.from(element)) {
    html2Canvas(element[index], opts).then(function (canvas) {
      // a4纸的尺寸[595.28,841.89]，html页面生成的canvas在pdf中图片的宽高
      const contentWidth = canvas.width;
      const contentHeight = canvas.height;
      const imgWidth = 595.28;
      const imgHeight = (592.28 / contentWidth) * contentHeight;
      const pageData = canvas.toDataURL("image/jpeg", 1.0);
      // 一页pdf显示html页面生成的canvas高度;
      const pageHeight = (contentWidth / 592.28) * 841.89;
      // 未生成pdf的html页面高度
      const leftHeight = contentHeight;
      pageArr[index] = {
        pageData: pageData,
        pageHeight: pageHeight,
        leftHeight: leftHeight,
        imgWidth: imgWidth,
        imgHeight: imgHeight,
      };
      if (++count === element.length) {
        // 转换完毕，可进行下一步处理 pageDataArr
        let counts = 0;
        for (const data of pageArr) {
          // 页面偏移
          let position = 0;
          // 转换完毕，save保存名称后浏览器会自动下载
          // 当内容未超过pdf一页显示的范围，无需分页
          if (data.leftHeight < data.pageHeight) {
            // addImage(pageData, 'JPEG', 左，上，宽度，高度)设置
            PDF.addImage(data.pageData, "JPEG", 0, 0, a4Width, a4Height);
          } else {
            // 超过一页时，分页打印（每页高度841.89）
            while (data.leftHeight > 0) {
              PDF.addImage(
                data.pageData,
                "JPEG",
                0,
                position,
                da4Width,
                a4Height
              );
              data.leftHeight -= data.pageHeight;
              position -= 841.89;
              if (data.leftHeight > 0) {
                PDF.addPage();
              }
            }
          }
          if (++counts === pageArr.length) {
            PDF.save(title + ".pdf");
          } else {
            // 未转换到最后一页时，pdf增加一页
            PDF.addPage();
          }
        }
      }
    });
  }
};
</script>

<style lang="scss" scoped>
.pdfDom {
  width: 595px !important;
  height: 842px !important;
  position: relative;
  page-break-after: always; /* 打印时分页 */
  background: white; /* 确保背景为白色 */
  box-sizing: border-box;
  margin: 0;
  padding: 20px;
}
.container {
  width: 100% !important;
  height: 100% !important;
  padding: 0 !important;
  margin: 0 !important;
}

/* 头部样式 */
.header {
  width: 100%;
  margin-bottom: 30px;
}

.title {
  font-size: 48px;
  font-weight: bold;
  color: #333;
}

/* 内容区域样式 */
.content {
  width: 100%;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.subtitle {
  margin-bottom: 40px;
  font-size: 18px;
  color: #666;
}

/* 报告卡片样式 */
.report-card {
  width: 100%;
  background-color: #fff;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  margin-bottom: 40px;
}

.report-title {
  display: block;
  font-size: 24px;
  font-weight: bold;
  color: #333;
  margin-bottom: 10px;
}

/* 信息网格样式 */
.info-grid {
  margin-top: 30px;
  width: 100%;
}

.info-row {
  display: flex;
  justify-content: space-between;
  padding: 15px 0;
  border-bottom: 1px solid #eee;
}

.info-label {
  font-size: 16px;
  color: #666;
}

.info-value {
  font-size: 16px;
  font-weight: 500;
  color: #333;
}

/* 页脚样式 */
.footer {
  font-size: 14px;
  color: #999;
  text-align: center;
  margin-top: 20px;
}
</style>
