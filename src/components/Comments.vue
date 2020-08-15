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


    <h3 class="commentAdd">Post Comment</h3>
    
    <b-form @submit="postComment">
      <b-form-group
        id="input-group-1"
        label="Name:"
        label-for="input-1"
        description="Enter your Name."
      >
        <b-form-input
          id="input-1"
          v-model="form.textName"
          placeholder="Enter your name"
          required></b-form-input>
      </b-form-group>

      <b-form-group
        id="textarea"
        label="Your Comment:"
        label-for="input-2"
      >
        <b-form-textarea
          id="textarea"
          v-model="form.textComment"
          placeholder="Write comment..."
          rows="3"
          max-rows="6"
          required
        ></b-form-textarea>
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
  </article>
</template>

<script>
export default {
  data() {
    return {
      comments: [],
      form: {
        textName: '',
        textComment: '',
        id: 6
      }
    }
  },
  methods: {
    postComment (event) {
      event.preventDefault()
      let newComment = {
        name: this.form.textName,
        body: this.form.textComment
      }

      this.comments.push(newComment)
      this.form.textName = ''
      this.form.textComment = ''
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
    line-height: 24px;
  }

  li h3:first-letter {
    text-transform: capitalize;
  }
  
  .comment-body:first-letter {
    text-transform: capitalize;
  }

  .commentAdd {
    margin-top: 20px;
  }
  
@media screen and (max-width: 768px) {
  h2 {
   font-size: 24px;
  }
  li h3 {
    font-size: 20px;
    line-height: 19px;
  }
  .comment-body {
    font-size: 16px;
    line-height: 18px;
  }

}
</style>