<template>
  <div class="container pt-1">
    <div class="card">
      <h2>Актуальные новости {{ now }}</h2>
      <span
        >Открыто: <strong>{{ openRate }}</strong> | Прочитано: <strong>{{ readRate }}</strong></span
      >
    </div>
  </div>
  <app-news
    v-for="item in news"
    :key="item.id"
    :title="item.title"
    :id="item.id"
    :is-open="item.isOpen"
    @open-news="openNews"
    @read-news="readNews"
    :wasRead="item.wasRead"
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
      readRate: 0,
      news: [
        {
          title: "News 1",
          id: 1,
          isOpen: false,
          wasRead: false,
        },

        {
          title: "News 2",
          id: 2,
          isOpen: false,
          wasRead: false,
        },

        {
          title: "News 3",
          id: 3,
          isOpen: false,
          wasRead: false,
        },
      ],
    };
  },

  methods: {
    openNews() {
      this.openRate++;
    },
    readNews(id) {
      let idx = this.news.findIndex(item => item.id === id);
      this.news[idx].wasRead = true;
      this.readRate++;
    },
  },
};
</script>

<style>
</style>
