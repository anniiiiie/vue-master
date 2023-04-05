<template>
  <div>
    <div class="post">
        <input  
      type="text"  
      placeholder="post name"
      v-model="post.title">
      <!-- V-MODELLL -->
      </div> 
      <div class="post">
        <input 
        type="text"  
        placeholder="post text"
        v-model="post.body" 
        >
        <!-- двойное связывание vyshe -->
      </div>
      <button class="post" @click="addPost">Post</button>
    </div>
</template>

<script>
export default {
    name:"post-form",
    data(){
        return {
            post:{
                title:'',
                body:'',
            },
        }
    },
    methods:{
        addPost(){
            this.$emit('add',this.post)
        },
    }

}
</script>

<style>

</style>