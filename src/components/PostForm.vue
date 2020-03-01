<template>
  <form v-if="!loading" class="form" v-on:submit="onsubmit">
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
</template>

<script>
export default {
  name:'PostForm',
  data(){
    return {
      loading: false,
      title: '',
      body:''
    }
  }

};
</script>

<style></style>
