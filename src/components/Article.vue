<template>
  <article class="col-sm-12">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><router-link :to="'/'">Home</router-link></li>
        <li class="breadcrumb-item active" aria-current="page">{{ post.title }}</li>
      </ol>
    </nav>
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
    this.$http.get(`http://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
      .then(response => response.json(), error => console.log(error))
      .then(json => this.post = json, error => console.log(error));
  }
}
</script>