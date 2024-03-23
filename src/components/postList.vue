<template>
    <div v-if="posts.length>0">
        <h3>PostList</h3>
        <transition-group name="list">
            <post-item v-for="post in posts"
            :post="post"
            :key="post.id"
            @remove="$emit('remove',post)"   
        />
        
        </transition-group>
   
       
    </div>
    <h2  v-else  style="color:red">
    Post list is empty
    </h2>
</template>
<script>
import postItem from './postItem.vue'
export default {
    components: {
        postItem
    },
    props: {
        posts: {
            type:Array,
            required:true,
        }
    }
}
</script>
<style scoped>
    
    .list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.6s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.list-move {
  transition: transform 0.6s ease;
}
</style>