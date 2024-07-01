<template>
  <div class="item">
    <!-- 设置插槽 -->
    <slot></slot>
  </div>
</template>

<script>
export default {};
</script>

<style lang="less">
.item {
  height: 5.125rem;
  margin: 0.25rem;
  background-image: url("../assets/bord.png"); /* 替换为你的图片路径 */
  background-size: cover; /* 调整图片大小以覆盖整个元素 */
  background-repeat: no-repeat; /* 防止图片重复 */
  background-position: center; /* 将图片居中对齐 */
}
</style>