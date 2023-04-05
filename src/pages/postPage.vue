<template>
  <div>
    {{ $router.currentRoute.params.id }}
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'postPage',
    data(){
        return{
            post: {}
        }
    },
    methods: {
        async getPost(postId){
            try{
                const response  = await axios.get(`https://jsonplaceholder.typicode.com/posts/${postId}`)
                this.post = response.data
                console.log(this.post)
            }
            catch(error){
                console.log('ERROR')
            }
        },
    },
    created(){
        this.getPost(this.$router.currentRoute.params.id)
    }
}
</script>

<style>

</style>