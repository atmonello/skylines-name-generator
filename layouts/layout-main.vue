<template>
  <div id="layout" class="container-fluid">
    <div class="row">
      <div id="title" class="col-12">
        <slot name="title"></slot>
      </div>
    </div>
    <div class="row">
      <div id="left" class="col-12 col-md-6">
        <slot name="selector"></slot>
      </div>
      <div id="right" class="col-12 col-md-6">
        <slot name="generator"></slot>
      </div>
    </div>
    <div class="row">
      <div id="footer" class="col-xs-12">
        <slot name="footer"></slot>
      </div>
    </div>
  </div>

</template>

<style lang="less" scoped>
#layout {
    background: #333333;
    min-height: 100vh;

    #left, #right {
      margin-bottom: 20px;
    }

    #footer {
      margin: 5px 0;
    }
}
</style>
