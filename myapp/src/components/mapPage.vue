<template>
  <div class="map" id="map"></div>
</template>

<script>
import axios from "axios";
import { onMounted, reactive, inject } from "vue";
import * as echarts from "echarts/core";
import {
  GeoComponent,
  TooltipComponent,
  VisualMapComponent,
  TitleComponent,
} from "echarts/components";
import { MapChart } from "echarts/charts";
import { CanvasRenderer } from "echarts/renderers";

echarts.use([
  GeoComponent,
  MapChart,
  CanvasRenderer,
  TooltipComponent,
  VisualMapComponent,
  TitleComponent,
]);

const provincesData = [
  { name: "北京", value: 144.722222 },
  { name: "天津", value: 115.022222 },
  { name: "河北", value: 234.755556 },
  { name: "山西", value: 359.7 },
  { name: "内蒙古", value: 2104.644444 },
  { name: "辽宁", value: 724.577778 },
  { name: "吉林", value: 1836.1 },
  { name: "黑龙江", value: 2958.955556 },
  { name: "上海", value: 199.711111 },
  { name: "江苏", value: 540.833333 },
  { name: "浙江", value: 1940.8 },
  { name: "安徽", value: 1408.411111 },
  { name: "福建", value: 2972.5 },
  { name: "江西", value: 3737.488889 },
  { name: "山东", value: 299.588889 },
  { name: "河南", value: 365.766667 },
  { name: "湖北", value: 1861.955556 },
  { name: "湖南", value: 2774.277778 },
  { name: "广东", value: 1641.166667 },
  { name: "广西", value: 4266.711111 },
  { name: "海南", value: 3633.477778 },
  { name: "重庆", value: 1889.822222 },
  { name: "四川", value: 3169.866667 },
  { name: "贵州", value: 3018.055556 },
  { name: "云南", value: 3926.355556 },
  { name: "西藏", value: 130104.677778 },
  { name: "陕西", value: 1121.111111 },
  { name: "甘肃", value: 1015.0 },
  { name: "青海", value: 13555.944444 },
  { name: "宁夏", value: 154.944444 },
  { name: "新疆", value: 3634.133333 },
];

export default {
  setup() {
    let $echarts = inject("echarts") || echarts;
    let mapData = reactive({});

    async function getState() {
      try {
        const response = await axios.get("/china/data");
        mapData = response.data;
      } catch (error) {
        console.error("Failed to fetch map data: ", error);
      }
    }

    onMounted(() => {
      console.log("Fetching map data...");
      getState().then(() => {
        console.log("Map data fetched.");
        $echarts.registerMap("china", mapData.chinaData);
        let myChart = $echarts.init(document.getElementById("map"));

        myChart.setOption({
          tooltip: {
            trigger: "item",
            formatter: function (params) {
              let province = provincesData.find(
                (prov) => prov.name === params.name
              );
              if (province) {
                return `${province.name}: ${province.value}`;
              }
              return "";
            },
          },
          geo: {
            map: "china",
            itemStyle: {
              areaColor: "#0099ff",
              borderColor: "#00ffff",
              shadowColor: "rgba(230,130,70,0.5)",
              shadowBlur: 30,
              emphasis: {
                focus: "self",
              },
            },
          },
          visualMap: {
            type: "continuous",
            min: 100,
            max: 5000,
            calculable: true,
            inRange: {
              color: ["#50a3ba", "#eac736", "#d94e5d"],
            },
            textStyle: {
              color: "#fff",
              top: "0px",
            },
            bottom: 0, // 将visualMap的底部与地图的最底部对齐
          },
          title: {
            left: "45%",
            text: "各省份总水资源",
            textStyle: {
              color: "#fff",
              fontSize: 15,
              textShadowBlur: 10,
              textShadowColor: "#33ffff",
            },
          },
          series: [
            {
              type: "map",
              map: "china",
              geoIndex: 0,
              data: provincesData.map((province) => ({
                name: province.name,
                value: province.value,
              })),
              itemStyle: {
                normal: {
                  areaColor: "blue", // 确保正常状态下的颜色
                  borderColor: "#00ffff",
                },
                emphasis: {
                  areaColor: "#2a333d", // 确保高亮状态下的颜色
                },
              },
            },
          ],
        });
      });
    });

    return {
      getState,
      mapData,
    };
  },
};
</script>

<style>
.map {
  width: 100%;
  height: 80%; /* 使图表高度减少 */
  margin-top: 0px; /* 增加顶部间距 */
}
</style>
