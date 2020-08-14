<template>
  <article class="col-sm-12">
    <h2>Comments</h2>
    <ul class="list-group">
      <li
        v-for="comment in comments"
        class="list-group-item"
        :key="comment.id"
      >
        <strong>{{ comment.name }}</strong> <em>wrote:</em> {{ comment.body }}
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
    this.$http.get(`http://jsonplaceholder.typicode.com/posts/${this.$route.params.id}/comments`)
      .then(response => response.json(), error => console.log(error))
      .then(json => this.comments = json, error => console.log(error));
  }
}
</script>