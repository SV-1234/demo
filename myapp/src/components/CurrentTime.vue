<template>
  <div class="current-time">{{ currentTime }}</div>
</template>
  
  <script>
export default {
  data() {
    return {
      currentTime: "",
    };
  },
  created() {
    this.updateCurrentTime();
    // Update the current time every second
    this.timer = setInterval(() => {
      this.updateCurrentTime();
    }, 1000);
  },
  beforeDestroy() {
    clearInterval(this.timer);
  },
  methods: {
    updateCurrentTime() {
      const date = new Date();
      this.currentTime = `${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`;
    },
  },
};
</script>
  
  <style scoped>
.current-time {
  font-size: 0.375rem;
  color: #3e92ce;
  margin-left: auto;
  line-height: 1rem;
  border: 1px solid #066fb5; /* 添加的边框样式 */
  padding: 0.5px; /* 内边距，使边框和文本之间有一些间距 */
}
</style>
  