<template>
  <div>
    <header>
      <h1>探究中国省份间水资源调度与防范</h1>
      <div class="gifImg">
        <span class="month-tip"></span>
      </div>
      <CurrentTime />
    </header>
    <!-- 大容器 -->
    <section class="container">
      <!-- 左容器 -->
      <section class="itemLeft">
        <ItemPage>
          <ItemOne />
        </ItemPage>
        <ItemPage>
          <ItemTwo />
        </ItemPage>
      </section>
      <!-- 中容器 -->
      <section class="itemCenter">
        <MapPage style="height: 400px" />

        <WordCloud style="height: 150px" />
      </section>
      <!-- 右容器 -->
      <section class="itemRight">
        <ItemPage>
          <ItemThree style="width: 400px; height: 300px" />
        </ItemPage>
        <ItemPage>
          <ItemFour style="width: 400px; height: 300px" />
        </ItemPage>
      </section>
    </section>
  </div>
</template>

<script>
import ItemPage from "@/components/itemPage.vue";
import ItemOne from "@/components/itemOne.vue";
import ItemTwo from "@/components/itemTwo.vue";
import ItemThree from "@/components/itemThree.vue";
import ItemFour from "@/components/itemFour.vue";
import MapPage from "@/components/mapPage.vue";
import CurrentTime from "@/components/CurrentTime.vue";
import WordCloud from "@/components/WordCloud.vue";
import { inject } from "vue";

export default {
  components: {
    ItemPage,
    ItemOne,
    ItemTwo,
    ItemThree,
    ItemFour,
    MapPage,
    CurrentTime,
    WordCloud,
  },

  setup() {
    let $echarts = inject("echarts");
    let $http = inject("axios");
    console.log($echarts);
    console.log($http);
  },
};
</script>

<style lang="less">
header {
  height: 1rem;
  width: 100%;
  // background-color: rgba(0, 0, 255, 0.2);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 0.5rem;
  position: relative;
}

header h1 {
  font-size: 0.375rem;
  color: #fff;
  line-height: 1rem;
  margin: 0;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}

.gifImg {
  width: 100%;
  height: 50%;
  position: absolute;
  top: 40%;
  min-height: 50px;
  overflow: hidden;
  text-align: center;
  &:after {
    content: "";
    top: 40%;
    left: 48%;
    transform: translate(-50%, 20%);
    display: block;
    position: absolute;
    width: 36.5%;
    min-width: 700px;
    height: 100%;
    background: url(../assets/header.gif) no-repeat center center;
    background-size: 100%;
  }
  .month-tip {
    margin-top: 3%;
    font-size: px2em(24, 32);
    color: #fff;
  }
}

// 大容器的样式
.container {
  // 最大最小的宽度
  min-width: 1200px;
  max-width: 2048px;
  margin: 0 auto;
  padding: 0.125rem 0.125rem 0;
  // background-color: gray;
  display: flex;
  // 设置左右在页面的份数
  .itemLeft,
  .itemRight {
    flex: 3;
  }
  .itemCenter {
    flex: 5;
    height: 10.5rpx;
    border: 1px solid blue;
    padding: 0.125rem;
    margin: 0.25rem;
    position: relative;
    padding: 0.5em 1.5em;
    border: none;
    background-color: transparent;
    cursor: pointer;
    outline: none;
    font-size: 18px;
  }
}
</style>
