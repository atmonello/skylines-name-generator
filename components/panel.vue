<template>
  <div class="panel">
    <div class="content">
      <slot name="content"></slot>
    </div>
  </div>
</template>

<style lang="less" scoped>
@import "../assets/vars.less";

.panel {
  background: #fff;
  border-radius: 5px;
  padding: 10px 20px;

  .content {
    width: 100%;
    height: 100%;
  }
}

</style>

<script>
export default {

};
</script>
