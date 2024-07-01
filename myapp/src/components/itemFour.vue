<template>
  <div>
    <div class="city">各省份-城市降雨量</div>
    <label for="province-select" style="margin-bottom: 20px"></label>
    <select
      id="province-select"
      v-model="selectedProvince"
      @change="updateChart"
      style="margin-top: 20px; margin-left: 30px"
    >
      <option
        v-for="province in radarData"
        :key="province.name"
        :value="province.name"
      >
        {{ province.name }}
      </option>
    </select>
    <div
      ref="radarChart"
      class="chart"
      style="width: 400px; height: 230px; margin-top: 15px"
    ></div>
  </div>
</template>

<script>
import * as echarts from "echarts";

export default {
  data() {
    return {
      selectedProvince: "安徽省",
      radarData: [
        {
          name: "安徽省",
          cities: [
            { name: "安庆市", value: 0.004035774 },
            { name: "蚌埠市", value: 0.00268952 },
            { name: "亳州市", value: 0.002517507 },
            { name: "池州市", value: 0.004465765 },
            { name: "滁州市", value: 0.002808025 },
            { name: "阜阳市", value: 0.002614162 },
            { name: "合肥市", value: 0.003094567 },
            { name: "淮北市", value: 0.002548452 },
            { name: "淮南市", value: 0.002731821 },
            { name: "黄山市", value: 0.004811158 },
            { name: "六安市", value: 0.003254585 },
            { name: "马鞍山市", value: 0.003374409 },
            { name: "宿州市", value: 0.002514574 },
            { name: "铜陵市", value: 0.003558666 },
            { name: "芜湖市", value: 0.003589003 },
            { name: "宣城市", value: 0.004162552 },
          ],
        },
        {
          name: "北京市",
          cities: [{ name: "北京市", value: 0.001634235 }],
        },
        {
          name: "福建省",
          cities: [
            { name: "福州市", value: 0.004297292 },
            { name: "龙岩市", value: 0.004286039 },
            { name: "南平市", value: 0.004755631 },
            { name: "宁德市", value: 0.004649078 },
            { name: "莆田市", value: 0.004010722 },
            { name: "泉州市", value: 0.003911457 },
            { name: "三明市", value: 0.004289565 },
            { name: "厦门市", value: 0.003683069 },
            { name: "漳州市", value: 0.003901894 },
          ],
        },
        {
          name: "甘肃省",
          cities: [
            { name: "白银市", value: 0.001030723 },
            { name: "定西市", value: 0.00192754 },
            { name: "甘南藏族自治州", value: 0.002607542 },
            { name: "嘉峪关市", value: 0.000354685 },
            { name: "金昌市", value: 0.000722677 },
            { name: "酒泉市", value: 0.000385054 },
            { name: "兰州市", value: 0.001170025 },
            { name: "临夏回族自治州", value: 0.001850339 },
            { name: "陇南市", value: 0.002884457 },
            { name: "平凉市", value: 0.001956556 },
            { name: "庆阳市", value: 0.001633496 },
            { name: "天水市", value: 0.002293954 },
            { name: "武威市", value: 0.000830771 },
            { name: "张掖市", value: 0.0011854 },
          ],
        },
        {
          name: "广东省",
          cities: [
            { name: "潮州市", value: 0.004079407 },
            { name: "东莞市", value: 0.004875575 },
            { name: "佛山市", value: 0.004856865 },
            { name: "广州市", value: 0.005249905 },
            { name: "河源市", value: 0.00404329 },
            { name: "惠州市", value: 0.004776197 },
            { name: "江门市", value: 0.004802741 },
            { name: "揭阳市", value: 0.003976871 },
            { name: "茂名市", value: 0.00478548 },
            { name: "梅州市", value: 0.003749038 },
            { name: "清远市", value: 0.005119062 },
            { name: "汕头市", value: 0.00361815 },
            { name: "汕尾市", value: 0.004427492 },
            { name: "韶关市", value: 0.004456676 },
            { name: "深圳市", value: 0.004907871 },
            { name: "阳江市", value: 0.004950579 },
            { name: "云浮市", value: 0.004306559 },
            { name: "湛江市", value: 0.004144085 },
            { name: "肇庆市", value: 0.005132649 },
            { name: "中山市", value: 0.00475389 },
            { name: "珠海市", value: 0.005143515 },
          ],
        },
        {
          name: "广西壮族自治区",
          cities: [
            { name: "百色市", value: 0.004498677 },
            { name: "北海市", value: 0.004604141 },
            { name: "崇左市", value: 0.004440316 },
            { name: "防城港市", value: 0.004685039 },
            { name: "贵港市", value: 0.005055655 },
            { name: "桂林市", value: 0.005757084 },
            { name: "河池市", value: 0.005755628 },
            { name: "贺州市", value: 0.005434442 },
            { name: "来宾市", value: 0.005409131 },
            { name: "柳州市", value: 0.006198446 },
            { name: "南宁市", value: 0.004987962 },
            { name: "钦州市", value: 0.004470586 },
            { name: "梧州市", value: 0.004898396 },
            { name: "玉林市", value: 0.004627979 },
          ],
        },
        {
          name: "贵州省",
          cities: [
            { name: "安顺市", value: 0.004256454 },
            { name: "毕节市", value: 0.003748472 },
            { name: "贵阳市", value: 0.004015226 },
            { name: "六盘水市", value: 0.004283789 },
            { name: "黔东南苗族侗族自治州", value: 0.004710542 },
            { name: "黔南布依族苗族自治州", value: 0.004756673 },
            { name: "黔西南布依族苗族自治州", value: 0.004159477 },
            { name: "铜仁市", value: 0.004720441 },
            { name: "遵义市", value: 0.004230292 },
          ],
        },
        {
          name: "海南省",
          cities: [
            { name: "白沙黎族自治县", value: 0.004189733 },
            { name: "保亭黎族苗族自治县", value: 0.004180205 },
            { name: "昌江黎族自治县", value: 0.003900484 },
            { name: "澄迈县", value: 0.004157204 },
            { name: "儋州市", value: 0.003694995 },
            { name: "定安县", value: 0.004390842 },
            { name: "东方市", value: 0.004171561 },
            { name: "海口市", value: 0.004224351 },
            { name: "乐东黎族自治县", value: 0.004424397 },
            { name: "临高县", value: 0.004080965 },
            { name: "陵水黎族自治县", value: 0.004324279 },
            { name: "琼海市", value: 0.004231145 },
            { name: "琼中黎族苗族自治县", value: 0.004290065 },
            { name: "三沙市", value: 0.004327926 },
            { name: "三亚市", value: 0.004325063 },
            { name: "屯昌县", value: 0.00415599 },
            { name: "万宁市", value: 0.0042397 },
            { name: "文昌市", value: 0.00421809 },
            { name: "五指山市", value: 0.004227889 },
          ],
        },
        {
          name: "河北省",
          cities: [
            { name: "保定市", value: 0.001764394 },
            { name: "沧州市", value: 0.001840303 },
            { name: "承德市", value: 0.001916874 },
            { name: "邯郸市", value: 0.001707409 },
            { name: "衡水市", value: 0.001791406 },
            { name: "廊坊市", value: 0.001902176 },
            { name: "秦皇岛市", value: 0.00192719 },
            { name: "石家庄市", value: 0.001793434 },
            { name: "唐山市", value: 0.001743184 },
            { name: "邢台市", value: 0.001790424 },
            { name: "张家口市", value: 0.001893684 },
          ],
        },
        {
          name: "黑龙江省",
          cities: [
            { name: "大庆市", value: 0.001054777 },
            { name: "大兴安岭地区", value: 0.001557527 },
            { name: "哈尔滨市", value: 0.001203706 },
            { name: "鹤岗市", value: 0.001208945 },
            { name: "黑河市", value: 0.001162172 },
            { name: "鸡西市", value: 0.001130913 },
            { name: "佳木斯市", value: 0.001075517 },
            { name: "牡丹江市", value: 0.001245117 },
            { name: "七台河市", value: 0.001200812 },
            { name: "齐齐哈尔市", value: 0.001155597 },
            { name: "双鸭山市", value: 0.001073396 },
            { name: "绥化市", value: 0.001132194 },
            { name: "伊春市", value: 0.001510957 },
          ],
        },
        {
          name: "河南省",
          cities: [
            { name: "安阳市", value: 0.001346324 },
            { name: "鹤壁市", value: 0.001265474 },
            { name: "焦作市", value: 0.00130535 },
            { name: "开封市", value: 0.001418162 },
            { name: "洛阳市", value: 0.001401794 },
            { name: "漯河市", value: 0.001409083 },
            { name: "南阳市", value: 0.001438494 },
            { name: "平顶山市", value: 0.001316714 },
            { name: "濮阳市", value: 0.001299883 },
            { name: "三门峡市", value: 0.001405316 },
            { name: "商丘市", value: 0.001386128 },
            { name: "新乡市", value: 0.001347545 },
            { name: "信阳市", value: 0.001444842 },
            { name: "许昌市", value: 0.001343577 },
            { name: "郑州市", value: 0.001463103 },
            { name: "周口市", value: 0.00135307 },
            { name: "驻马店市", value: 0.001376473 },
          ],
        },
        {
          name: "香港特别行政区",
          cities: [{ name: "香港", value: 0.003199949 }],
        },
        {
          name: "湖北省",
          cities: [
            { name: "鄂州市", value: 0.002093005 },
            { name: "恩施土家族苗族自治州", value: 0.002250326 },
            { name: "黄冈市", value: 0.002047467 },
            { name: "黄石市", value: 0.00199619 },
            { name: "荆门市", value: 0.002111779 },
            { name: "荆州市", value: 0.002019775 },
            { name: "潜江市", value: 0.002053865 },
            { name: "神农架林区", value: 0.002312759 },
            { name: "十堰市", value: 0.002023336 },
            { name: "随州市", value: 0.002134588 },
            { name: "天门市", value: 0.00208918 },
            { name: "武汉市", value: 0.002136412 },
            { name: "仙桃市", value: 0.002133015 },
            { name: "咸宁市", value: 0.002042723 },
            { name: "襄阳市", value: 0.002073499 },
            { name: "孝感市", value: 0.002054035 },
            { name: "宜昌市", value: 0.002265938 },
          ],
        },
        {
          name: "湖南省",
          cities: [
            { name: "长沙市", value: 0.003481239 },
            { name: "常德市", value: 0.003604063 },
            { name: "郴州市", value: 0.003486547 },
            { name: "衡阳市", value: 0.003449215 },
            { name: "怀化市", value: 0.003595313 },
            { name: "娄底市", value: 0.00345259 },
            { name: "邵阳市", value: 0.003597938 },
            { name: "湘潭市", value: 0.003444031 },
            { name: "湘西土家族苗族自治州", value: 0.003679475 },
            { name: "益阳市", value: 0.003523496 },
            { name: "永州市", value: 0.003585478 },
            { name: "岳阳市", value: 0.003550129 },
            { name: "张家界市", value: 0.003603538 },
            { name: "株洲市", value: 0.003409536 },
          ],
        },
        {
          name: "吉林省",
          cities: [
            { name: "白城市", value: 0.000621191 },
            { name: "白山市", value: 0.000789792 },
            { name: "长春市", value: 0.000760868 },
            { name: "吉林市", value: 0.000755571 },
            { name: "辽源市", value: 0.000722021 },
            { name: "四平市", value: 0.000722331 },
            { name: "松原市", value: 0.000688038 },
            { name: "通化市", value: 0.000739901 },
            { name: "延边朝鲜族自治州", value: 0.000741719 },
          ],
        },
        {
          name: "江苏省",
          cities: [
            { name: "常州市", value: 0.002180789 },
            { name: "淮安市", value: 0.002201186 },
            { name: "连云港市", value: 0.002179937 },
            { name: "南京市", value: 0.002253179 },
            { name: "南通市", value: 0.002241737 },
            { name: "苏州市", value: 0.002227618 },
            { name: "宿迁市", value: 0.002162099 },
            { name: "泰州市", value: 0.002188692 },
            { name: "无锡市", value: 0.002233093 },
            { name: "徐州市", value: 0.002204788 },
            { name: "盐城市", value: 0.002194213 },
            { name: "扬州市", value: 0.00222284 },
            { name: "镇江市", value: 0.002191517 },
          ],
        },
        {
          name: "江西省",
          cities: [
            { name: "抚州市", value: 0.003245844 },
            { name: "赣州市", value: 0.003313567 },
            { name: "吉安市", value: 0.003342404 },
            { name: "景德镇市", value: 0.003180226 },
            { name: "九江市", value: 0.003201335 },
            { name: "南昌市", value: 0.003194307 },
            { name: "萍乡市", value: 0.003162285 },
            { name: "上饶市", value: 0.003296512 },
            { name: "新余市", value: 0.003138292 },
            { name: "宜春市", value: 0.003206217 },
            { name: "鹰潭市", value: 0.00313088 },
          ],
        },
        {
          name: "辽宁省",
          cities: [
            { name: "鞍山市", value: 0.00129233 },
            { name: "本溪市", value: 0.001347112 },
            { name: "朝阳市", value: 0.001308007 },
            { name: "大连市", value: 0.001308671 },
            { name: "丹东市", value: 0.001315973 },
            { name: "抚顺市", value: 0.001334492 },
            { name: "阜新市", value: 0.001353438 },
            { name: "葫芦岛市", value: 0.001344369 },
            { name: "锦州市", value: 0.001341989 },
            { name: "辽阳市", value: 0.001343384 },
            { name: "盘锦市", value: 0.001282308 },
            { name: "沈阳市", value: 0.001304487 },
            { name: "铁岭市", value: 0.001291194 },
            { name: "营口市", value: 0.001321329 },
          ],
        },
        {
          name: "内蒙古自治区",
          cities: [
            { name: "阿拉善盟", value: 0.002164125 },
            { name: "巴彦淖尔市", value: 0.002105351 },
            { name: "包头市", value: 0.00214783 },
            { name: "赤峰市", value: 0.002060582 },
            { name: "鄂尔多斯市", value: 0.002151347 },
            { name: "呼和浩特市", value: 0.002124008 },
            { name: "呼伦贝尔市", value: 0.002099944 },
            { name: "通辽市", value: 0.002064059 },
            { name: "乌海市", value: 0.002151906 },
            { name: "乌兰察布市", value: 0.002120728 },
            { name: "锡林郭勒盟", value: 0.002191981 },
            { name: "兴安盟", value: 0.002043738 },
          ],
        },
        {
          name: "宁夏回族自治区",
          cities: [
            { name: "固原市", value: 0.004148183 },
            { name: "石嘴山市", value: 0.00408232 },
            { name: "吴忠市", value: 0.004141317 },
            { name: "银川市", value: 0.004129055 },
            { name: "中卫市", value: 0.004102597 },
          ],
        },
        {
          name: "青海省",
          cities: [
            { name: "果洛藏族自治州", value: 0.002868053 },
            { name: "海北藏族自治州", value: 0.002844283 },
            { name: "海东市", value: 0.00291359 },
            { name: "海南藏族自治州", value: 0.002884412 },
            { name: "海西蒙古族藏族自治州", value: 0.002878857 },
            { name: "黄南藏族自治州", value: 0.00283623 },
            { name: "西宁市", value: 0.002833733 },
            { name: "玉树藏族自治州", value: 0.002850151 },
          ],
        },
        {
          name: "山东省",
          cities: [
            { name: "滨州市", value: 0.001651746 },
            { name: "德州市", value: 0.001665464 },
            { name: "东营市", value: 0.001633141 },
            { name: "菏泽市", value: 0.001682012 },
            { name: "济南市", value: 0.001706293 },
            { name: "济宁市", value: 0.00164366 },
            { name: "莱芜市", value: 0.001676492 },
            { name: "聊城市", value: 0.00168249 },
            { name: "临沂市", value: 0.001693499 },
            { name: "青岛市", value: 0.00169065 },
            { name: "日照市", value: 0.00166064 },
            { name: "泰安市", value: 0.001655188 },
            { name: "威海市", value: 0.001651187 },
            { name: "潍坊市", value: 0.001651871 },
            { name: "烟台市", value: 0.001652784 },
            { name: "枣庄市", value: 0.001620297 },
            { name: "淄博市", value: 0.001647614 },
          ],
        },
        {
          name: "山西省",
          cities: [
            { name: "长治市", value: 0.001398381 },
            { name: "大同市", value: 0.001452214 },
            { name: "晋城市", value: 0.001437949 },
            { name: "晋中市", value: 0.001432604 },
            { name: "临汾市", value: 0.001422446 },
            { name: "吕梁市", value: 0.001436798 },
            { name: "朔州市", value: 0.001423104 },
            { name: "太原市", value: 0.001442897 },
            { name: "忻州市", value: 0.001451207 },
            { name: "阳泉市", value: 0.001457799 },
            { name: "运城市", value: 0.001426406 },
          ],
        },
      ],
    };
  },
  mounted() {
    this.initChart();
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$refs.radarChart);
      this.updateChart();
    },
    updateChart() {
      const province = this.radarData.find(
        (p) => p.name === this.selectedProvince
      );
      const option = {
        title: {},
        tooltip: {},

        radar: {
          indicator: province.cities.map((city) => ({
            name: city.name,
            max: 0.005,
          })),
        },
        series: [
          {
            name: province.name,
            type: "radar",
            data: [
              {
                value: province.cities.map((city) => city.value),
                name: province.name,
                itemStyle: {
                  color: "#73C0DE",
                },
                lineStyle: {
                  color: "#73C0DE",
                },
                areaStyle: {
                  color: "rgba(0, 0, 255, 0.3)", // 透明度为 0.3 的紫色
                },
              },
            ],
          },
        ],
      };
      this.chart.setOption(option);
    },
  },
};
</script>

<style>
#province-select {
  margin-left: auto;
}
.city {
  margin-top: 30px;
  text-align: center;
  padding-top: 20px;
  color: white;
  font-size: 14px;
}

.chart {
  height: 4.5rem;
}
</style>
