<template>
  <section id="app">
    <div>
      <comment-form @add-com="addDo" />
      <comment-list @del-com="delDo" :comments="comments" />
    </div>
  </section>
</template>

<script>
import CommentForm from "./components/comment-form.vue";
import CommentList from "./components/comment-list.vue";
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      comments: [],
    };
  },
  methods: {
    addDo(comment) {
      axios({
        url: " /api/comment/add",
        method: "post",
        params: {
          author: comment.author,
          body: comment.body,
        },
        responseType: "json",
      }).then((data) => {
        this.comments.push(comment);
      });
    },
    delDo(b) {
      axios({
        url: " /api/comment/del",
        method: "get",
        params: {
          body: b,
        },
        responseType: "json",
      }).then((data) => {
        this.comments = this.comments.filter((e) => e.body != b);
      });
    },
  },
  components: {
    CommentForm,
    CommentList,
  },
  created() {
    axios({
      url: " /api/comment/list",
      responseType: "json",
    }).then((data) => {
      this.comments = data.data;
    });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
