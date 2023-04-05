<template>
    <div>
    <div
    v-if="posts.length ===0">Tut nicho net</div>
    <div  v-for="(post,id) in posts"
    :key="id" 
    class="new" 
    >
    <div></div>
      <h4>Title: {{ post.title }}</h4>
      <p @click="showDetails(post.id)"><strong>Text:</strong>{{ post.body }}</p>
      <button 
        @click="deletePost(id)" 
        >
        delete
      </button>
      </div>
    </div>
</template>

<script>
export default {
    name:'post-list',
    props:{
        posts:{
            type:Array,
            default(){
                return []
            },
            required:false,
        },
    },
     methods:{
        deletePost(id){
            this.$emit('del',id)
        },
        showDetails(postId){
            this.$router.push({
                name: 'post',
                params: {
                    id: postId
                }
            })
        }
    },
}
</script>

<style>

</style>