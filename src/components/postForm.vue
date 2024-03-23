

<template >
    <div>
        <form @submit.prevent>
            <h3>Post Creation</h3>
            <myinput 
            v-model="post.title"
             type="text" 
             placeholder="Post tittle"/>
            <myinput v-model="post.body"
              type="text" 
              placeholder="Post description"/>
              
            <mybtn style="align-self: center;" @click="createPost"  class="btn">Add post</mybtn>
        </form>
    </div>
</template>
<script>


export default {
 
   
    data(){
        return {
            post:{
                title:'',
                body:'',
            }
        }
    },
    methods:{
        createPost() {
            this.post.id=Date.now(),
           this.$emit('create',this.post)
            this.post = {
                title:'',
                body:'',
            }
       }
    }
}
</script>
<style scoped>
   
    form{
        display: flex;
        flex-direction: column;
    }
    
.btn{ 
    margin-top: 12px;
    width: 40%;
}
  
</style>