<template>
  <div
    class="flip_card md:flip-card-md"
    :class="{ active: flipped }"
    :href="url"
    target="_blank"
  >
    <div class="container">
      <div class="front">
        <slot name="image"></slot>
        <slot name="front"> </slot>
      </div>
      <div class="back">
        <slot name="back"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FlipCard",
  props: ["url"],
  data: function () {
    return {
      flipped: false,
    };
  },
  methods: {
    flipCard() {
      this.flipped = !this.flipped;
    },
    flipMobile() {
      this.flipped = !this.flipped;
    },
  },
};
</script>

<style type="text/css" scoped>
.container {
  -ms-transform-style: preserve-3d;
  transform-style: preserve-3d;
  -webkit-transform-style: preserve-3d;
  perspective: 1000px;
  -webkit-perspective: 1000px;
  width: 100%;
  height: 100%;
}

.front,
.back {
  height: 100%;
  width: 90%;
  margin: 0 auto;
  @apply rounded-lg;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  -ms-transition: transform 0.7s cubic-bezier(0.4, 0.2, 0.2, 1);
  transition: transform 0.7s cubic-bezier(0.4, 0.2, 0.2, 1);
  -webkit-transition: transform 0.7s cubic-bezier(0.4, 0.2, 0.2, 1);
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  background: #fafafa !important;
}

.front .image {
  position: absolute;
  height: 100%;
  @apply rounded-lg;
  width: 100%;
  background-size: cover !important;
  background-position: center center;
  top: 0;
  left: 0;
}

.front {
  -ms-transform: rotateY(0deg);
  -webkit-transform: rotateY(0deg);
  transform: rotateY(0deg);
  -webkit-transform-style: preserve-3d;
  -ms-transform-style: preserve-3d;
  background: #fff !important;
  transform-style: preserve-3d;
  padding-top: 10px;
}

.back {
  position: absolute;
  top: 0;
  left: 5%;
  width: 90%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: #fff !important;
  @apply rounded-lg pt-4 overflow-hidden;
  transform: rotateY(180deg);
  transform-style: preserve-3d;
}

.back h3 {
  @apply text-xl font-bold text-left w-full pt-1 pb-2 mx-auto border-b;
  width: 80%;
}
</style>
