<template>
  <section>
    <div>
      <input v-model="author" />
      <input v-model="body" />
      <button v-on:click="addComment">add</button>
    </div>
  </section>
</template>

<script>
export default {
  props: [],
  data() {
    return {
      author: "",
      body: "",
    };
  },
  methods: {
    addComment: function () {
      this.$emit("add-com", {
        author: this.author,
        body: this.body,
      });
      this.body = "";
      this.author = "";
    },
  },
};
</script>