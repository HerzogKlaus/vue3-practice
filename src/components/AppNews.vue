<template>
  <div class="card">
    <h3>{{ title }}</h3>
    <button class="btn" @click="open">{{ isNewsOpen ? "Закрыть" : "Открыть" }}</button>
    <div v-if="isNewsOpen">
      <hr />
      <p>Lorem ipsum dolor sit amet.</p>
      <button v-if="!wasRead" class="btn primary" @click="read">Прочитано</button>
    </div>
  </div>
</template>

<script>
export default {
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
  },
};
</script>