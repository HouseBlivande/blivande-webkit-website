<template>
  <div
    class="w-full"
    :style="elementStyle(data.style.container, 'container')"
    :class="elementClass(data.style.container.class)"
  >
    <div v-for="(view, index) in data.views" :key="index">
      <Hero
        v-if="view.hero"
        :data="view.hero"
        :config="view.hero.config"
        :globalStyle="globalStyleSheet"
        :stylesheet="data.style"
        ref="childComponent"
      />
    </div>
  </div>
</template>

<script>
import Hero from "@/components/views/Hero.vue";

export default {
  components: {
    Hero,
  },
  props: ["data", "globalStyle", "index"],
};
</script>

<style scoped lang="scss">
.hero {
  @apply border-b;
  background-attachment: fixed !important;
}
</style>
