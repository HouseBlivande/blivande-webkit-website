<template>
  <div
    class="section md:section-md"
    id="partners"
  >
    <div
      class="flex font-bold justify-between items-center mx-auto mt-12"
      v-if="data.title"
      :style="textStyle('title', data.style)"
    >
      <h1 class="m-0 p-0 w-full text-center" :class="titleClassSize(data.style)">
        {{ data.title }}
      </h1>
    </div>
    <div
      class="wrapper md:wrapper-md mx-auto"
    >
      <div class="view_partners md:view_partners-md">
        <a
          class="partner md:partner-md"
          v-for="item in data.content"
          :key="item.title"
          :href="item.url"
          target="_blank"
        >
          <img :src="item.logo" />
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    wrapperObj() {
      var wrapperObj = {
        maxWidth: "",
      };
      if (this.stylesheet && this.stylesheet.wrapper) {
        wrapperObj["maxWidth"] = this.stylesheet.wrapper;
      }
      if (this.data.style && this.data.style.wrapper) {
        wrapperObj["maxWidth"] = this.data.style.wrapper;
      }
      return wrapperObj;
    },
  },
  props: ["data", "stylesheet", "globalStyle"],
};
</script>

<style lang="scss">
@responsive {
  .view_partners {
    @apply block mx-auto h-auto mt-3 pb-12;
    column-count: 2;
  }

  .view_partners-md {
    @apply block mx-auto h-auto mt-3 pb-12;
    column-count: 3;
  }


  .partners_wrapper {
    @apply flex flex-row justify-between my-4;
  }

  .partners_wrapper-md {
    @apply flex flex-row justify-between my-4;
  }

  .partner {
    @apply flex flex-col py-6 items-center justify-center;
    page-break-inside: avoid;
    width: 100%;
    img {
      max-width: 80%;
      margin: 0 auto;
    }
  }
  .partner-md {
    @apply flex flex-col py-6 items-center justify-center;
    height: 200px;
    page-break-inside: avoid;
    img {
      max-width: 40%;
      margin: auto;
    }
  }

  .box {
    @apply inline-block w-full border border-gray-200 mb-4;
    a {
      @apply text-2xl m-0;
    }
  }
}
</style>
