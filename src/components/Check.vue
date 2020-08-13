<template>
  <div class="input-container">
    <h1 class="mb-3">Wejapa Countries</h1>
    <!-- <div id="post">
      {{ titles }}
    </div> -->
  </div>
</template>

<script>
var fetch = require("node-fetch");

export default {
  data() {
    return {
      titles: []
    };
  },
  mounted () {
    this.getPost();
    this.showTitles();
  },
  methods: {
    async getPost() {
      let postResponse = await fetch(`http://jsonplaceholder.typicode.com/posts`);
      
      let post = await postResponse.json();
      post.forEach((element) => {
        this.titles.push({
          key: element.id,
          title: element.title
        })
      })
      // post = this.titles;
      
    },
    showTitles() {
      console.log(this.titles);
    }
  },
};
</script>

<style scoped>
</style>