<template>
  <article class="post-article col-sm-12 col-lg-8">
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
.post-article {
  margin-top: 80px;
}
h1 {
  text-align: left;
  width: 70%;
  
}
p {
  text-align: left;
  width: 70%;

}
</st