<template>
  <div>
    <div class="row">
      <div class="col s6">
        <PostForm @postCreated="addPost"/>
      </div>
    </div>
    <div class="row">
      <div class="col s6" v-for="(post, index) in posts" v-bind:item="post" :index="index"
           :key="post.id">
        <div class="card">
          <div class="card-content">
            <p class="card-title">
              {{ post.title }}
            </p>
            <p class="timestamp">{{post.createdAt}}</p>
          </div>
          <div class="card-action">
            <a href="#" @click="editPost(post)">Edit</a>
            <a href="#" class="delete-btn" @click="deletePost(post.id)">Delete</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import PostService from '../PostService';
  import PostForm from '../components/PostForm.vue';
  const postService = new PostService();

  export default {
    name:"Home",
    components:{
      PostForm
    },
    data(){
      return {
        posts:[]
      }
    },
    methods:{
      addPost(post) {
        this.posts.unshift(post)
      }
    },
    created(){
      postService.getAllPosts()
        .then(res => {
          this.posts = res.data;
          console.log(this.posts);
        })
        .catch(err => console.error(err));
    }
  }
</script>

<style scoped>
  .card . card-contant .card-title{
    margin-bottom: 0;
  }

  .card . card-contant p.timestamp{
    color: #999;
    margin-bottom: 10px;
  }

  .delete-btn{
    color: red !important;
  }

</style>
