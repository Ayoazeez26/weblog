<template>
  <article class="col-sm-12 col-lg-8">
    <h1>{{ post.title }}</h1>
    <p> {{ post.body }}</p>

    <Comments />
  </article>
</template>

<script>
import Comments from './Comments.vue'

export default {
  components: {
    Comments
  },
  data() {
    return {
      post: {}
    }
  },
  created() {
    this.$http.get(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
      .then(response => response.json(), error => console.log(error))
      .then(json => this.post = json, error => console.log(error));
  }
}
</script>

<style scoped>
h1 {
  text-align: left;
}
p {
  text-align: left;

}
</style>