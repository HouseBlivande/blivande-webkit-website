<template>
  <div class="section md:section-md" :style="containerStyle(data.style)">
    <div
      class="flex font-bold justify-between items-center mx-auto"
      v-if="data.title"
      :style="textStyle('title', data.style)"
    >
      <h3 class="m-0 p-0 w-full" :class="titleClassSize(data.style)">
        {{ data.title }}
      </h3>
      <!-- div class="toggle_menu" v-if="data.views && data.views.length > 1">
        <div v-for="(view, index) in getViews(data.views)"
          class="toggle"
          :class="[view, {active: activeView == view}]"
          @click="toggleView(view)"
          :key="index"
        ></div>
      </div -->
    </div>
    <div v-for="(view, index) in data.views" :key="index">
      <TextView
        v-if="view.text && ready"
        class="wrapper md:wrapper-md py-4 pb-2 mx-auto"
        :stylesheet="view.style"
        :data="view.text"
      />

      <Grid
        v-if="topics && view.grid && activeView == 'grid' && ready"
        v-bind:data="topics"
        :config="view.grid"
      >
        <template v-slot:item="{ item }">
          <GridItem>
            <template>
              <div slot="content">
                <a :href="item.url" target="_blank">
                    <div
                      class="item_image"
                      :style="{ background: 'url(' + getImgUrl(item) + ')' }"
                    ></div>
                  <div class="item_excerpt" v-html="'<strong>' + item.title + '</strong>' + '<br>' + item.excerpt.slice(0,200) + '...'"></div>
                </a>
              </div>
              <div slot="footer">
                <div class="item_meta">
                  <a
                    class="item_favs"
                    v-if="show(view.grid.display, 'favourites')"
                    :href="item.url"
                    target="_blank"
                    >{{ item.like_count }}</a
                  >
                  <a
                    class="item_replies"
                    v-if="show(view.grid.display, 'replies')"
                    :href="item.url"
                    target="_blank"
                    >{{ item.reply_count }}</a
                  >
                </div>
              </div>
            </template>
          </GridItem>
        </template>
      </Grid>

      <Row
        v-if="topics && view.cards && activeView == 'cards' && ready"
        :topics="topics"
        :stylesheet="data.style"
        :display="view.cards.display"
      />
    </div>
  </div>
</template>

<script>
import Grid from "@/components/views/Grid.vue";
import GridItem from "@/components/views/GridItem.vue";
import TextView from "@/components/views/Text.vue";

import Row from "@/components/ui/Row.vue";
import axios from "axios";
import moment from "moment";

export default {
  props: ["data", "stylesheet", "baseUrl", "globalStyle"],
  data() {
    return {
      topics: null,
      full_width: false,
      reset: 0,
      ready: false,
      activeView: "",
    };
  },
  components: {
    TextView,
    Grid,
    GridItem,
    Row,
  },
  created() {
    this.activeView = this.getViews(this.data.views)[0];
    if (this.data.config.view) {
      this.activeView = this.data.config.view;
    }
    if (this.data.config.tag) {
      this.getTopics(this.data.config.tag, "tags");
    }
    if (this.data.config.category) {
      this.getTopics(this.data.category, "category");
    }
  },
  methods: {
    show(array, property) {
      if (array.includes(property)) {
        return true;
      } else {
        return false;
      }
    },
    getTopics(value, filter) {
      axios
        .get(
          `${this.baseUrl}/webkit_components/topics.json?${filter}=${value}&per=500&serializer=event`
        )
        .then(({ data }) => {
          var topics = data;
          if (this.data.config.sort_by) {
            topics = this.sortBy(
              data,
              this.data.config.sort_by.property,
              this.data.config.sort_by.order
            );
          }
          this.topics = topics;
          this.ready = true;
        });
    },
    getImgUrl(item) {
      if (item.image_url) {
        return item.image_url
      } else {
        let match = item.cooked.match(/(img src=")([^\s\\]*)/gi)[0].replace('img src="','').replace('"','')
        return this.baseUrl + match
      }
    },
    getViews(data) {
      return data.reduce(function (result, view) {
        if (Object.keys(view)[0] !== "text") {
          result.push(Object.keys(view)[0]);
        }
        return result;
      }, []);
    },
    sortBy(data, value, order) {
      var ord_val = -1;
      if (order == "ascending") {
        ord_val = 1;
      }
      var sorted = data.sort((a, b) =>
        a[value] > b[value] ? ord_val : b[value] > a[value] ? -ord_val : 0
      );
      return sorted;
    },
    toggleView(value) {
      this.activeView = value;
    },
  },
  filters: {
    formatDate: function (value) {
      return moment(String(value)).format("dddd, MMMM Do YYYY");
    },
  },
};
</script>
<style lang="scss">

.item_favs {
  @apply font-bold mt-0 p-3 pl-6 pr-4 text-sm;
  color: rgba(0, 0, 0, 0.7);
  text-decoration: none !important;
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 45.8 54.7'%3E%3Cpath fill='rgba(0,0,0,0.7)' d='M9.6 27.3a2.1 2.1 0 01.6 1.9L8 41.3a2 2 0 003 2.2l10.9-5.8a2.1 2.1 0 012 0l10.9 5.8a2 2 0 003-2.2l-2.1-12.1a2.1 2.1 0 01.6-2l8.9-8.5a2.1 2.1 0 00-1.2-3.6l-12.2-1.6a2.1 2.1 0 01-1.6-1.2L24.8 1.2a2.1 2.1 0 00-3.8 0l-5.3 11.1a2.1 2.1 0 01-1.7 1.2L1.8 15a2.1 2.1 0 00-1.2 3.6z' data-name='Calque 2'/%3E%3C/svg%3E")
    no-repeat 15px 56%;
  background-size: 14px;
  padding-left: 35px;
}

.item_replies {
  @apply border-gray-200 font-bold p-3 pl-6 pr-4 text-sm;
  color: rgba(0, 0, 0, 0.7);
  text-decoration: none !important;
  background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' data-name='Layer 1' viewBox='0 0 512 640'%3E%3Cpath fill='rgba(0,0,0,0.7)' d='M512 396v26c-3 7-5 14-11 19-18 14-43 7-52-15-9-24-26-39-48-50-30-15-63-21-96-23l-78-1a23 23 0 00-3 0v62a39 39 0 01-2 11c-6 22-34 33-55 12L15 284c-7-6-13-13-15-22v-12c2-9 8-16 15-22l87-87 66-66c10-11 23-14 36-8s20 17 20 31v62h7c6 0 58 1 105 13 28 7 73 19 109 50 66 57 67 150 67 173z'/%3E%3C/svg%3E")
    no-repeat 15px 56%;
  background-size: 14px;
  padding-left: 35px;
}

.item_meta {
  @apply flex items-center bg-gray-100 overflow-hidden border-t border-gray-200;
  height: 45px;
  a {
    @apply border-l;
    &:nth-child(1) {
      border: none;
    }
  }
}
</style>
