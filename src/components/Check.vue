<template>

  <div class="input-container">
    <h1 class="mb-3">Trending Topics</h1>
    <div
      id="post-title"
      ref="postList"
      v-for="post in displayedPosts"
      :key="post.key"
      :value="post.title"
      :per-page="perPage"
    >
    {{ post.title }}
    </div>
    <nav aria-label="Page navigation example">
            <ul class="pagination">
                <li class="page-item">
                    <button
                      type="button"
                      class="page-link"
                      v-if="page != 1"
                      @click="page--"
                      >
                        Previous
                      </button>
                </li>
                <li class="page-item">
                    <button
                      type="button"
                      class="page-link"
                      v-for="pageNumber in pages.slice(page-1, page+5)"
                      @click="page = pageNumber"
                      :key="pageNumber"
                    >
                      {{ pageNumber }}
                    </button>
                </li>
                <li class="page-item">
                    <button type="button" @click="page++" v-if="page < pages.length" class="page-link"> Next </button>
                </li>
            </ul>
        </nav> 
  </div>
</template>

<script>
var axios = require('axios');

export default {
  static: {
  },
  data() {
    return {
      posts: [],
      perPage: 10,
      page: 1,
      pages: []
    };
  },
  mounted () {
    axios
      .get(`http://jsonplaceholder.typicode.com/posts`)
      .then(response => (this.getPosts(response.data)))
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
    numPages() {
      let numOfPages = Math.ceil(this.posts.length / this.perPage);
      for (let index = 1; index <= numOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate (posts) {
      let page = this.page;
      let perPage = this.perPage;
      let from = (page * perPage) - perPage;
      let to = (page * perPage);
      return posts.slice(from, to);
    }
  },
  computed: {
    displayedPosts () {
      return this.paginate(this.posts);
    }
  },
  watch: {
    posts () {
      this.numPages();
    }
  },
  created() {
    this.getPosts();
  }
};
</script>

<style scoped>
  .input-container {
    width: 70%;
    margin: 0 auto;
    margin-top: 60px;
  }
  #post-title {
    text-transform: uppercase;
    height: 50px;
    background: #ddd;
    margin: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 10px;
    padding: 10px;
  }
  button.page-link {
    display: inline-block;
  }
  button.page-link {
    font-size: 20px;
    color: #29b3ed;
    font-weight: 500;
  }
</style>