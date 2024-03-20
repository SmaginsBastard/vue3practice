<template>
    <select v-model="modelValue" @change="changeOptions">
        <option disabled  value="">choose option</option>
        <option v-for="option in options" :key="option.value"  :value="option.value"> 
        {{ opention.name }}
        </option>
    </select>
</template>
<script>
export default {
    name: 'myselect',
    props: {
        modelValue: {
            type: String,
        },
        options: {
            type: Array,
            default: () => []
        }
    },
    methods
    changeOptions(event) {
        this.$emit('update:modelValue', event.target.value)
    }
}
</script>
<style scoped>
    
</style>