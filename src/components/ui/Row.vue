<template>
  <div class="row md:row-md">
    <div class="card_row md:card_row-md" ref="content" v-if="topics">
      <Card
        v-for="item in topics"
        :key="item.id"
        ref="flipCard"
        :url="item.url"
        class="card topic md:card-md"
      >
        <template slot="image">
          <div
            class="image"
            :style="{ backgroundImage: 'url(' + item.image_url + ')' }"
          ></div>
        </template>
        <template slot="front">
          <a
            :href="item.url"
            target="_blank"
          >
            <div class="topic_data">
              <div class="topic_title" v-if="show('title')">
                <h2 :style="uiStyle('highlight', stylesheet)">
                  {{ item.title.split(".")[1] }}
                </h2>
              </div>
            </div>
          </a>
        </template>
        <template slot="back">
          <div
            class="card_excerpt"
            :style="textStyle('paragraph', stylesheet)"
            v-html="item.excerpt.split('.')[0] + '.'"
          ></div>
          <a
            class="card_footer"
            :style="uiStyle('action', stylesheet)"
            :href="item.url"
            target="_blank"
            >Tell me more!</a
          >
        </template>
      </Card>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import Card from "@/components/ui/FlipCard.vue";
export default {
  props: ["users", "topics", "display", "globalStyle", "stylesheet"],
  components: {
    Card
  },
  data() {
    return {
      flip: false,
    };
  },
  methods: {
    strippedCooked(cooked) {
      let stripped = cooked.replace(/(<span([^>].*)<\/span>)/gi, "");
      return stripped.replace(/(<([^>]+)>)/gi, "");
    },
    show(value) {
      return this.display.includes(value);
    },
    toggleCard() {
      this.$refs.flipCard.flipMobile();
    },
    scroll() {
      this.$nextTick(() => {
        this.$refs.content.scrollLeft += 1000;
      });
    },
  },
  filters: {
    formatDate: function (value) {
      return moment(String(value)).format("MM/DD/YY");
    },
  },
};
</script>

<style lang="scss"></style>
