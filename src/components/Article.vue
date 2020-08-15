<template>
  <article class="post-article col-sm-12 col-lg-8">
    <h2>{{ post.title }}</h2>
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
  text-align: left;
  width: 70%;
  margin: 0 auto;
  margin-top: 60px;
}
h2 {
  text-align: left;
  text-transform: capitalize;
}
p {
  font-size: 20px;
}
p:first-letter {
text-transform: capitalize;
}

@media screen and (max-width: 768px) {
  h2 {
   font-size: 26px;
  }
  .post-article {
    width: 100%;
    margin-top: 40px;
  }
  p {
    line-height: 20px;
    font-size: 16px;
  }
}
</style>