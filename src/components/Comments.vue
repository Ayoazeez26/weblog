<template>
  <article class="col-sm-12">
    <h2>Comments</h2>
    <ul class="list-group">
      <li
        v-for="comment in comments"
        class="list-group-item"
        :key="comment.id"
      >
        <h3><strong>{{ comment.name }}</strong></h3>
        <p class="comment-body">{{ comment.body }}</p>
      </li>
    </ul>
  </article>
</template>

<script>
export default {
  data() {
    return {
      comments: {}
    }
  },
  mounted() {
    this.$http.get(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}/comments`)
      .then(response => response.json(), error => console.log(error))
      .then(json => this.comments = json, error => console.log(error));
  }
}
</script>

<style scoped>
  li h3 {
    font-size: 22px;
    text-align: left;
  }

  .comment-body {
    font-size: 18px;
    text-align: left;
  }
</style>