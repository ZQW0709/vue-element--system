<template>
  <div class="main-layout">
    <div>
      <slot name="header"></slot>
    </div>
    <div>
      <slot name="footer"> </slot>
    </div>
  </div>
</template>
<script>
export default {}
</script>
<style lang="scss" scoped>
.main-layout {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
}
</style>
