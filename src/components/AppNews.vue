<template>
  <div class="card">
    <h3>{{ title }}</h3>
    <button class="btn" @click="open">{{isNewsOpen ? 'Закрыть' : 'Открыть'}}</button>
    <p v-if="isNewsOpen">Lorem ipsum dolor sit amet.</p>
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
  },
  data() {
    return {
      isNewsOpen: this.isOpen,
    };
  },
  methods: {
    open() {
      this.isNewsOpen = !this.isNewsOpen;
      if (this.isNewsOpen) {
        this.$emit("open-news", 1337);
      }
    },
  },
};
</script>