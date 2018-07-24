<template>
  <div class="hello mt-3 container">
    <ul class="list-unstyled">
      <li class="media m-3" v-for="post in posts" :key="post.title">
        <div>
          
        </div>
        <img :src="post.data.thumbnail" alt="ggf" class="mr-3">
        <div class="media-body">
          <h5 class="mt-0 mb-1"><a :href="createLink(post.data.permalink)" target="_blank">{{post.data.title}}</a></h5>
          <p>
            <h3 class="text-danger">{{post.data.ups}} ⬆</h3>
            <p>created {{formatDate(post.data.created_utc)}} ago</p>
            <span class="badge badge-pill badge-secondary">{{post.data.num_comments}} comments</span>
            
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { parse, distanceInWords } from 'date-fns'

export default {
  name: 'Posts',
  data() {
    return {
      posts : []
    };
  },
  mounted(){
    this.load()
  },
  methods :{
    load(){
      //fetch posts
      const url = 'https://www.reddit.com/r/rarepuppers/.json'
      fetch(url)
        .then(response => response.json())
        .then(result => {
          console.log(result.data.children);
          this.posts = result.data.children
        })
    },
    formatDate(date){
      return distanceInWords(parse(date * 1000), new Date())
    },
    createLink(path){
      return `https://www.reddit.com${path}`
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
