<template>
  <div id="app">
    <h1>helllo</h1>
    <post-form 
      @add="addPost"
    ></post-form>
    <input placeholder="find post" v-model="find" >
    <select
      v-model="sortType">
      <option>
        Choose the type
      </option>
      <option>
        Name
      </option>
      <option>
        Soderjanie
      </option>
    </select>
    <h2>Post list</h2>
    <!-- передаем свойство компьютед -->
     <!-- searchPosts -->
    <post-list :posts="searchAndSortedPosts"
 
    
    @del="deletePost">     
    </post-list>
      
  </div>
</template>

<script>
import postList from "@/components/post-list.vue"
import postForm from "@/components/post-form.vue"
import axios from 'axios'


export default {
  components: { postList, postForm },
  name: 'postsPage',
  data(){
    return {
      posts : [ ],
      title: '',
      text: '',
      find:'',
      sortType:'',
    }
  },
  computed:{
    searchPosts(){
      let searchedPosts = []
      for (const post of this.posts){
        if (post.title.includes(this.find) || post.body.includes(this.find)){
          searchedPosts.push(post)
        }
      }
      return searchedPosts;
    },
    searchAndSortedPosts(){
      const searchedPostsCopy = [...this.searchPosts]
      if (this.sortType === 'Name'){
        return searchedPostsCopy.sort((post1,post2) => {
          return post1.title.localeCompare(post2.title)
        })
      }
      else if (this.sortType === 'Soderjanie'){
        return searchedPostsCopy.sort((post1,post2) =>{
          return post1.body.localeCompare(post2.bpdy)
        })
      }
      else{
        return searchedPostsCopy
      }
    },
  },
  methods:{
    addPost(post){
      console.log(post)
      this.posts.push({
        ...post
      })
      post.body=''
      post.title=''
    },
    deletePost(id){
      this.posts.splice(id,1)
    },
    async getPosts(){
      const url = 'https://jsonplaceholder.typicode.com/posts'
      try{
        let response = await axios.get(url)
        console.log(response)
        this.posts = response.data
    }
    catch(error){
      console.error('error')
    }
  },
},
watch:{
  // sortType(newValue, oldValue){
  //   console.log('sortType value depended')
  //   console.log(`New value is ${newValue}`)
  //   console.log(`old value is ${oldValue}`)
    // if (newValue === 'Name'){
    //   this.posts = this.posts.sort((post1,post2) => {
    //     return post1.title > post2.title
    //   })
    // }
    // else if (newValue === 'Soderjanie'){
    //   this.posts = this.posts.sort((post1,post2) => {
    //     return post1.body>post2.body
    //   })
    // }
  // }
  // функция в воч отслеживает значение одноименной переменной
  // по умолчанию первый аргумент это новое зн а второй это старое
},
async created(){
  console.log('created')
  await  this.getPosts()
},
mounted(){
  console.log('mounted')
},
beforeUpdate(){
  console.log('b4 upd')
},
updated(){
  console.log('ud')
},
beforeDestroy(){
  console.log('it will be dead')
},
destroyed(){
  console.log('f ')
}
}  
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 40px;}

</style>