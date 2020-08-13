<template>
  <div class="input-container">
    <h1 class="mb-3">Trending Topics</h1>
    <div
      id="post-title"
      v-for="post in posts"
      :key="post.key"
      :value="post.title"
      :per-page="perPage"
      :current-page="currentPage"
    >
      {{ post.title }}
    </div>
    <a @click="prevPage" id="btn-prev" ref="prev">Prev</a>
    <a @click="nextPage" id="btn-next" ref="next">Next</a>
    <p>Page: <span id="page"></span></p>
  </div>
</template>

<script>
var axios = require('axios');

export default {
  data() {
    return {
      posts: [],
      perPage: 10,
      currentPage: 1
    };
  },
  mounted () {
    axios
      .get(`http://jsonplaceholder.typicode.com/posts`)
      .then(response => (this.getPosts(response.data)))
      .then(this.getPosts());
  },
  methods: {
    getPosts(response) {
      response.forEach((element) => {
        this.posts.push({
          key: element.id,
          title: element.title
        })
      })
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
        this.changePage(this.currentPage);
      }
    },
    nextPage() {
      if (this.currentPage < this.numPages()) {
        this.currentPage++;
        this.changePage(this.currentPage);
      }
    },
    numPages() {
      return Math.ceil(this.posts.length / this.perPage)
    },
    changePage(page) {
      console.log(this.$refs.prev, page);
    }
  },
  computed: {
    rows() {
      return this.posts.length
    }
  }
};
</script>

<style scoped>
  .input-container {
    background-color: #ddd;
    width: 70%;
    margin: 0 auto;
  }
  #post-title {
    text-transform: uppercase;
    height: 50px;
    background: #fff;
    margin: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  a {
    cursor: pointer;
    display: block;
    padding: 5px;
    margin-bottom: 10px;
  }
</style>