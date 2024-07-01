<template>
  <div>
    <h2>平均用水排行</h2>
    <div class="chart" id="myEchartsTwo">图表的容器</div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");
    let emitter = inject("emitter");

    let data = reactive({});

    async function getState() {
      data = await $http({ url: "/two/data" });
    }

    onMounted(() => {
      getState().then(() => {
        let myChart = $echarts.init(document.getElementById("myEchartsTwo"));
        myChart.setOption({
          animation: true, // 开启动画
          animationDuration: 2000, // 动画持续时间，单位毫秒
          animationEasing: "cubicInOut", // 动画缓动效果类型
          tooltip: {
            trigger: "axis",
            axisPointer: {
              type: "cross",
              label: {
                backgroundColor: "#e6b600",
              },
            },
          },
          legend: {
            textStyle: {
              color: "#fff",
            },
            data: [
              "江苏",
              "安徽",
              "江西",
              "广东",
              "黑龙江",
              "四川",
              "河南",
              "山东",
            ],
          },
          grid: {
            left: "1%",
            right: "4%",
            bottom: "3%",
            containLabel: true,
          },
          xAxis: {
            type: "category",
            boundaryGap: false,
            data: data.data.chartTwo.chartData.day,
            axisLine: {
              lineStyle: {
                color: "#fff",
              },
            },
          },
          yAxis: {
            type: "value",
            axisLine: {
              lineStyle: {
                color: "#fff",
              },
            },
          },
          series: [
            {
              name: "江苏",
              type: "line",
              data: data.data.chartTwo.chartData.num.江苏,
              showSymbol: false,
              lineStyle: { color: "rgb(128, 255, 165)" },
              emphasis: { focus: "series" },
            },
            {
              name: "安徽",
              type: "line",
              data: data.data.chartTwo.chartData.num.安徽,
              showSymbol: false,
              lineStyle: { color: "rgb(0, 221, 255)" },
              emphasis: { focus: "series" },
            },
            {
              name: "江西",
              type: "line",
              data: data.data.chartTwo.chartData.num.江西,
              showSymbol: false,
              lineStyle: { color: "rgb(55, 162, 255)" },
              emphasis: { focus: "series" },
            },
            {
              name: "广东",
              type: "line",
              data: data.data.chartTwo.chartData.num.广东,
              showSymbol: false,
              lineStyle: { color: "rgb(255, 0, 135)" },
              emphasis: { focus: "series" },
            },
            {
              name: "黑龙江",
              type: "line",
              data: data.data.chartTwo.chartData.num.黑龙江,
              showSymbol: false,
              lineStyle: { color: "rgb(255, 191, 0)" },
              emphasis: { focus: "series" },
            },
            {
              name: "四川",
              type: "line",
              data: data.data.chartTwo.chartData.num.四川,
              showSymbol: false,
              lineStyle: { color: "rgb (255, 255, 255)" },
              emphasis: { focus: "series" },
            },
            {
              name: "河南",
              type: "line",
              data: data.data.chartTwo.chartData.num.河南,
              showSymbol: false,
              lineStyle: { color: "rgb(128, 255, 0)" },
              emphasis: { focus: "series" },
            },
            {
              name: "山东",
              type: "line",
              data: data.data.chartTwo.chartData.num.山东,
              showSymbol: false,
              lineStyle: { color: "rgb(11, 0, 0)" },
              emphasis: { focus: "series" },
            },
          ],
        });

        myChart.on("mouseover", function (params) {
          if (params.seriesName) {
            emitter.emit("provinceHover", params.seriesName);
          }
        });

        myChart.on("mouseout", function () {
          emitter.emit("provinceHover", null);
        });
      });
    });
    return {
      getState,
      data,
    };
  },
};
</script>

<style>
h2 {
  height: 0.6rem;
  color: #fff;
  line-height: 0.6rem;
  font-size: 0.25rem;
  text-align: center;
}
.chart {
  height: 4.5rem;
}
</style>
