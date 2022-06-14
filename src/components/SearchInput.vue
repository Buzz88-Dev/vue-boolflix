<template>
    <div>
        <button @click.prevent="resetSearch()">Clear</button>
        <input type="text" placeholder="Search" v-model="inputText" @keyup.enter="$emit('mySearch', inputText)" >
    </div>
</template>

<script>
export default {
    name: 'SearchInput',

    data(){
        return {
            inputText : "",           
        }
    },

    methods: {
        resetSearch(){
            this.inputText = "";
            this.$emit('mySearch', this.inputText);
        }
    }
}
</script>

<style  scoped lang="scss">

    
</style>