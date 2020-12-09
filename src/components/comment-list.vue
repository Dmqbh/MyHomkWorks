<template>
  <section>
    <div v-for="c in comments" :key="c.id">
      <span>{{ c.author }}</span>
      <span>{{ c.body }}</span>
      <a href="#" v-on:click="delComment(c.body)">del</a>
    </div>
  </section>
</template>

<script>
export default {
  props: ["comments"],
  data() {
    return {};
  },
  methods: {
    delComment: function (body) {
      this.$emit("del-com", body);
    },
  },
};
</script>