<template >
    
    <button class="btn">

     <slot> default</slot>
    </button>
</template>
<script>
export default {
    name: 'mybtn',
}
</script>
<style scoped>
    .btn{
        background-color: teal;
        color: white;
        border: none;
        padding: 10px 15px;
        cursor: pointer;
        border-radius: 5px;  
    
        
    }  
</style>