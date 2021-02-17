<template>
  <div class="card">
    <h3>{{ title }}</h3>
    <app-btn @action="open">{{ isNewsOpen ? "Закрыть" : "Открыть" }}</app-btn>
    <div v-if="isNewsOpen">
      <hr />
      <p>Lorem ipsum dolor sit amet.</p>
      <app-btn v-if="!wasRead" color="primary" class="btn primary" @action="read">Прочитано</app-btn>
      <app-btn color="danger" class="btn danger" v-if="wasRead" @action="readBack"> Отметить непрочитанной</app-btn>
      <app-news-list></app-news-list>
    </div>
  </div>
</template>

<script>
import AppBtn from "./AppBtn";
import AppNewsList from "./AppNewsList";
export default {
  components: {
    AppBtn,
    AppNewsList,
  },
  props: {
    title: {
      type: String,
      required: true,
    },
    id: {
      type: Number,
      required: true,
    },
    isOpen: {
      type: Boolean,
      required: false,
      default: true,
      validator(value) {
        console.log(value);
        return true;
      },
    },
    wasRead: {
      type: Boolean,
      required: false,
      default: true,
    },
  },
  emits: {
    "open-news": null,
    "read-news"(id) {
      if (id) {
        return true;
      }
      console.warn("Нет параметра id");
      return false;
    },
    "read-back": null,
  },
  data() {
    return {
      isNewsOpen: this.isOpen,
      isNewsRead: this.wasRead,
    };
  },
  methods: {
    open() {
      this.isNewsOpen = !this.isNewsOpen;
      if (this.isNewsOpen) {
        this.$emit("open-news");
      }
    },

    read() {
      this.isNewsOpen = false;
      this.$emit("read-news", this.id);
    },

    readBack() {
      this.$emit("read-back", this.id);
    },
  },
};
</script>