<template>
  <div class="hero_container">
    <div
      class="hero_standard md:hero_standard-md"
      :style="elementStyle(data.style.wrapper, 'wrapper')"
      :class="elementClass(data.style.wrapper.class)"
    >
      <div class="hero_content md:hero_content-md">
        <div class="hero_title flex flex-col md:hero_title-md">
          <h1
            v-if="data.title"
            v-html="data.title"
          ></h1>
        </div>
        <div class="hero_actions md:hero_actions-md">
          <a
            v-for="item in data.buttons"
            :style="uiStyle('button', data.style)"
            :class="getClass('button', data.style)"
            :href="item.url"
            :key="item.url"
          >
            {{ item.text }}
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  props: ["data"],
};
</script>

<style scoped lang="scss">
.hero {
  @apply border-b;
  background-attachment: fixed !important;
}

.hero_container {
  @apply inline-block w-full;
}

.hero_content {
  @apply w-full;
}

@responsive {
  .hero_content {
    @apply w-full;
  }
  .hero_container {
    margin: 0;
    background: url("https://forum.blivande.com/uploads/blivande/original/1X/ce80eedb75991fa72b48a15ceb9ca803d15bc64b.jpeg");
    background-position: 15% 40%;
    background-attachment: fixed;
  }
  .hero_standard {
    @apply flex flex-row h-screen w-screen items-end justify-end p-8;
    margin: 0 auto;
    .hero_title-md {
      padding: 0;
    }
  }
  .hero_actions {
    @apply w-full mb-10 mt-10;
    text-align: center;
    display: inline-block !important;
    a {
      width: auto !important;
      max-width: 100px !important;
    }
  }
  .content_wrapper {
    @apply inline-block;
  }
  .hero_image {
    @apply inline-block;
  }
  .hero_title {
    @apply flex font-display text-3xl max-w-2xl mx-auto pl-0 pb-1 mb-4;
    text-align: center;
    color: white;
    font-weight: 300;
    text-shadow: 1px 1px #000000;
    font-family: "Raleway", "Times", serif
  }
  .hero_description {
    @apply text-lg mt-2 mx-12;
    white-space: pre-wrap;
  }

  .hero_standard-md {
    @apply flex flex-row h-screen w-screen items-end justify-end;

    align-items: flex-end !important;

    img {
      width: 80%;
    }
    .content_wrapper {
      @apply flex;
    }
  }
  .hero_actions-md {
    @apply w-full mb-10 mt-10;
    text-align: center;
    a {
      width: auto !important;
    }
  }
}
</style>
