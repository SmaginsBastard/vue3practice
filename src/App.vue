<template>
    
<div class="app">
        <input type="text" v-model.trim="modificatorlValue">
       <h1>Page with posts</h1>
       <myinput
       v-model="searchQuery"
       placeholder="search..."
       />
       <div class="app__btns">
        <mybtn @click="showDialog" style="margin: 15px 0;"> create post </mybtn>
        <myselect  v-model="selectedSort" :options="sortOptions" > 
            
        </myselect>
       </div>
     
<mydialog  v-model:show="dialogVisible" > 
    <postForm 
@create="createPost"/>

</mydialog>


    
<postList :posts="sortAndSearchPosts" 
@remove="removePost"
v-if="!isPostLoading"/>

<div v-else>Идет загрузка...</div>
</div>
</template>


<script>
import axios from 'axios';
import postForm from './components/postForm.vue'
import postList from './components/postList.vue'
import Myinput from './components/UI/myinput.vue';
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
        searchQuery: '',
        selectedSort: '',
        sortOptions: [
            { value: 'title', name: 'By name' },
            { value: 'body', name: 'By description' },
        ]   
            
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

computed: {
    sortedposts(){
      return[...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },
    sortAndSearchPosts() {
        return this.sortedposts.filter((post) => post.title.includes(this.searchQuery))
    }
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