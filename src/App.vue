<template>
  <div class="site_container">
    <div v-if="globalStyleSheet">
      <div v-for="(section, index) in sections" :key="index" :id="section.id">
        <component
          v-bind:is="section.type"
          :key="componentKey + index"
          :baseUrl="$globals.config.baseUrl"
          :globalStyle="globalStyleSheet"
          :data="section"
          :index="index"
        ></component>
      </div>
    </div>
  </div>
</template>

<script src="js-yaml.min.js"></script>
<script>
import Header from "@/components/core/Header.vue";
import Events from "@/components/core/Events.vue";
import Topics from "@/components/core/Topics.vue";
import Partners from "@/components/core/Partners.vue";
import Terms from "@/components/core/Terms.vue";
import Content from "@/components/core/Content.vue";

export default {
  name: "home",
  data() {
    return {
      componentKey: 0
    };
  },
  components: {
    Header,
    Events,
    Topics,
    Partners,
    Terms,
    Content
  },
  created() {
    this.getData();
  },
};
</script>
<style lang="scss">
.site_container {
  @apply flex flex-col w-full;
  overflow-x: hidden;
}
</style>
