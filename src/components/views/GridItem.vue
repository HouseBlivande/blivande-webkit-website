<template>
  <div class="grid_item bg-white">
    <div class="header"><slot name="header"></slot></div>
    <div class="content"><slot name="content"></slot></div>
    <div class="footer"><slot name="footer"></slot></div>
  </div>
</template>

<script>
export default {
  name: "GridItem",
};
</script>
<style lang="scss">
.grid_item {
  @apply inline-block w-full border border-gray-200 rounded-lg mb-4 overflow-hidden;
  .header {
    @apply px-4 w-full border-gray-200;
    a {
      @apply w-full pt-3 inline-block pb-2 font-bold;
    }
    .item_date {
      @apply inline-block text-sm border-t w-full border-gray-200 m-0 py-2 leading-tight;
      color: rgba(0, 0, 0, 0.4);
    }
  }
  .content {
    @apply text-sm;
    .item_image {
      @apply w-full;
      height: 200px;
      background-size: cover !important;
      background-position: 50% 50% !important;
    }
    .item_excerpt {
      @apply px-4 py-3;
      height: 170px;
      overflow: hidden;
    }
  }
}
</style>
