<template>
  <div>
    <h2>水灾区域面积</h2>
    <div class="chart" id="myEcharts">图表的容器</div>
  </div>
</template>

<script>
import { inject, onMounted, reactive } from "vue";
export default {
  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");

    let data = reactive({});

    async function getState() {
      data = await $http({ url: "/three/data" });
    }

    onMounted(() => {
      getState().then(() => {
        console.log("饼状图", data);

        let myChart = $echarts.init(document.getElementById("myEcharts"));
        myChart.setOption({
          legend: {
            top: "bottom",
            textStyle: {
              color: "#fff", // 修改图例 name 的字体颜色为白色
            },
          },
          tooltip: {
            show: true,
          },
          series: [
            {
              type: "pie",
              data: data.data.chartThree.chartData,
              radius: [5, 70],
              center: ["50%", "45%"],
              roseType: "area",
              itemStyle: {
                borderRadius: 10,
              },
              label: {
                textStyle: {
                  color: "#fff", // 修改扇区标签文字颜色为白色
                },
              },
            },
          ],
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
  height: 2.25rem;
}
</style>