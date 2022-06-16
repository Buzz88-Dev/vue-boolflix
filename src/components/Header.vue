<template>
    <div class="header">
        <div>
            <h3>BOOLFIX</h3>
        </div>
        <div>
            <!-- <button @click.prevent="resetSearch()">Clear</button> -->
            <input type="text" placeholder="Search" v-model="inputText" @keyup.enter="$emit('mySearch', inputText)" >
        </div>       
    </div>
</template>

<script>
export default {
    name: 'HeaderInput',

    data(){
        return {
            inputText : "",           
        }
    },

    methods: {
        resetSearch(){
            this.inputText = "";
        }
    }
}
</script>

<style  scoped lang="scss">

    .header {
        width: 80%;
        margin: auto;
        display: flex;
        justify-content: space-between;
        height: 100px;
        align-items: center;

        h3 {
            color: red;
            font-size: 30px;
        }

        input {
            height: 30px;
        }
    }

</style>