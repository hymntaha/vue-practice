<template>
  <form v-if="!loading" class="form" v-on:submit.prevent="onsubmit">
    <div class="input-field">
      <label for="title">Title</label>
      <input type="text" name="title" v-model="title" class="validate" />
      <span class="helper-text" data-error="Title must not be empty"></span>
    </div>
    <div class="input-field">
      <label for="body">Title</label>
      <input type="text" name="body" v-model="body" class="validate">
      <span class="helper-text" data-error="Body must not be empty"></span>

    </div>
    <button class="waves-effect waves-light btn"></button>
  </form>
  <div class="progress" v-else-if="loading">
    <div class="indeterminate">
    </div>
  </div>
</template>

<script>
  import PostService from '../PostService';

  const postService = new PostService();

export default {
  name:'PostForm',
  data(){
    return {
      loading: false,
      title: '',
      body:'',
      errors:{}
    }
  },
  methods{
    onSubmit(){
      this.loading = true;
      if (!this.validForm()) {
        this.loading = false
        return;
      }
      const post = {
        title: this.title,
        body: this.body
      };

      postService.writePost(post)
        .then(res => {
          this.loading = false;
          this.body = '';
          this.title = '';
          console.log(res.data);
        })
        .catch(err => console.error(err));
    },
    validForm(){
      this.errors = {};
      if (this.title.trim() === '') {
        this.errors.title = 'Title '
      };
      if (this.body.trim() === '') {
        this.errors.body = 'Body'
      };

      if (Object.keys(this.errors).length > 0) {
        return false;
      } else return true;
    }
  }

};
</script>

<style>
  .form{
    margin: 50px;
  }
  .progress{
    margin:100px 0;
  }
</style>
