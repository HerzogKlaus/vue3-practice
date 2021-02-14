<template>
  <div class="container pt-1">
    <div class="card">
      <h2>Актуальные новости {{ now }}</h2>
      <span>Открыто {{ openRate }}</span>
    </div>
  </div>
  <app-news
    v-for="item in news"
    :key="item.id"
    :title="item.title"
    :id="item.id"
    :is-open="item.isOpen"
    @open-news="openNews"
  ></app-news>
</template>
 
<script>
import AppNews from "./components/AppNews";
export default {
  components: {
    "app-news": AppNews,
  },
  data() {
    return {
      now: new Date().toLocaleDateString(),
      openRate: 0,
      news: [
        {
          title: "News 1",
          id: 1,
          isOpen: false,
        },

        {
          title: "News 2",
          id: 2,
          isOpen: false,
        },

        {
          title: "News 3",
          id: 3,
          isOpen: false,
        },
      ],
    };
  },

  methods: {
    openNews(data) {
      this.openRate++;
      console.log(data);
    },
  },
};
</script>

<style>
</style>
