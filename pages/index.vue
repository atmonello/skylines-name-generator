<template>
  <div id="index">
    <layout>
      <title-container slot="title"></title-container>
      <type-selector slot="selector"></type-selector>
      <name-generator slot="generator"></name-generator>
      <page-footer slot="footer"></page-footer>
    </layout>
  </div>
</template>

<script>
/* eslint-disable import/no-unresolved */
import layout from "~/layouts/layout-main.vue";
import titleContainer from "~/components/title.vue";
import typeSelector from "~/templates/typeSelector.vue";
import nameGenerator from "~/templates/nameGenerator.vue";
import footer from "~/components/footer.vue";

export default {
  components: {
    layout,
    "title-container": titleContainer,
    "type-selector": typeSelector,
    "name-generator": nameGenerator,
    "page-footer": footer,
  },
};
</script>
