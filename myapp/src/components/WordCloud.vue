<template>
  <div>
    <!-- 新增文本框 -->
    <div class="title" style="text-align: center">多降雨量省份</div>

    <div ref="wordCloud" style="width: 600px; height: 200px"></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import "echarts-wordcloud";

export default {
  name: "WordCloud",
  data() {
    return {
      wordCloudData: [], // 用于存储筛选后的数据，供词云图使用
    };
  },
  mounted() {
    this.processData();
  },
  methods: {
    processData() {
      // 示例数据，需替换为你的实际数据
      const data = [
        { year: 2018, province: "安徽省", value: 3.414695 },

        { year: 2018, province: "福建省", value: 4.025741 },
        { year: 2018, province: "广东省", value: 4.767945 },

        { year: 2018, province: "广东省", value: 4.767945 },
        { year: 2018, province: "广东省", value: 4.767945 },
        { year: 2018, province: "广东省", value: 4.767945 },
        { year: 2018, province: "广西", value: 5.045084 },
        { year: 2018, province: "广西", value: 5.045084 },
        { year: 2018, province: "广西", value: 5.045084 },
        { year: 2018, province: "广西", value: 5.045084 },
        { year: 2018, province: "广西", value: 5.045084 },
        { year: 2018, province: "广西", value: 5.045084 },

        { year: 2018, province: "海南省", value: 5.255322 },
        { year: 2018, province: "河南省", value: 2.245509 },
        { year: 2018, province: "黑龙江省", value: 1.895783 },

        { year: 2018, province: "湖南省", value: 4.196918 },
        { year: 2018, province: "青海省", value: 1.607905 },

        { year: 2018, province: "云南省", value: 4.42231 },

        { year: 2018, province: "广东省", value: 4.767945 },
        { year: 2018, province: "广东省", value: 4.767945 },
        { year: 2019, province: "福建省", value: 0.004573661 },
        { year: 2019, province: "甘肃省", value: 0.001258132 },
      ];

      const provinceCount = {};
      data.forEach((entry) => {
        const province = entry.province;
        if (!provinceCount[province]) {
          provinceCount[province] = 0;
        }
        provinceCount[province]++;
      });

      // 调试输出: 显示统计的省份及其出现次数
      console.log("Province count:", provinceCount);

      // 获取出现次数最多的前十个省份
      const sortedProvinces = Object.entries(provinceCount)
        .sort((a, b) => b[1] - a[1])
        .slice(0, 10);

      // 调试输出: 显示排序后的前十个省份
      console.log("Sorted Provinces:", sortedProvinces);

      // 更新数据，映射为echarts所需的格式
      this.wordCloudData = sortedProvinces.map(([name, value]) => ({
        name,
        value,
      }));

      // 立即绘制词云图
      this.drawWordCloud();
    },
    drawWordCloud() {
      const chart = echarts.init(this.$refs.wordCloud);
      const option = {
        tooltip: {
          show: true,
          formatter: function (params) {
            return `${params.name}: ${params.value}`;
          },
        },
        series: [
          {
            type: "wordCloud",
            gridSize: 20, // 控制词云图的清晰度
            sizeRange: [12, 50],
            rotationRange: [-90, 90],
            shape: "circle",
            textStyle: {
              normal: {
                color: function () {
                  return `rgb(${Math.round(Math.random() * 255)}, ${Math.round(
                    Math.random() * 255
                  )}, ${Math.round(Math.random() * 255)})`;
                },
              },
              emphasis: {
                shadowBlur: 10,
                shadowColor: "#333",
              },
            },
            data: this.wordCloudData, // 确保使用筛选后的数据
          },
        ],
      };
      chart.setOption(option);
      window.addEventListener("resize", () => {
        chart.resize();
      });
    },
  },
};
</script>

<style scoped>
.title {
  color: #73c0de;
  font-size: 20px; /* 根据需要调整字体大小 */
  margin-bottom: 20px; /* 添加底部外边距以与图表保持一定距离 */
}
</style>
