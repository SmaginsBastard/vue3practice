<template>

    <div class="post">
        <div>
            <div><strong>name:{{post.title}}</strong></div>
        <div><strong>description:{{post.body}}</strong></div>
        </div>
      <div class="post__btns">
<mybtn @click="$emit('remove', post)"> Remove</mybtn>
      

</div>

  </div>
   
</template>
<script>
export default {

    
    
props: {
post: {
        type:Object,
        required:true,
    }
},

}

</script>

<style scoped>
    .post{
        padding: 15px;
        border: 1px solid teal;
        margin-top: 15px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .post__btns{
        margin-bottom: 5px;
       
    }

    .btn{ 
      
        
    }
</style>