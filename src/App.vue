<template>
    
<div class="app">
        <input type="text" v-model.trim="modificatorlValue">
       <h1>Page with posts</h1>
       <div class="app__btns">
        <mybtn @click="showDialog" style="margin: 15px 0;"> create post </mybtn>
        <myselect> </myselect>
       </div>
     
<mydialog  v-model:show="dialogVisible" > 
    <postForm 
@create="createPost"/>

</mydialog>


    
<postList :posts="posts" 
@remove="removePost"
v-if="!isPostLoading"/>

<div v-else>Идет загрузка...</div>
</div>
</template>


<script>
import axios from 'axios';
import postForm from './components/postForm.vue'
import postList from './components/postList.vue'
export default {

    components: { 
        postForm,
        postList,
        
       
        
    },
    data() {
        return {
         posts: [],
        dialogVisible: false,
        modificatorlValue: '',  
        isPostLoading: false,
            
        }
    },

    mounted() {
    this.fetchPosts();
},
    methods: {
      
        createPost(post) {
                this.posts.push(post)     
                this.dialogVisible = false        
        },
        removePost(post) {
            this.posts= this.posts.filter((p) => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true
        },
        async fetchPosts() {
            try {
                this.isPostLoading = true
             const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
             this.posts = response.data
             
            }
            catch(e) {
                alert('Error')
            } finally {
                this.isPostLoading = false
            }
        },
 
    },
}
</script>
<style>
    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .app {

        padding: 20px;
    }
   
   .app__btns{
       display: flex;
       justify-content: space-between;
   }

</style>