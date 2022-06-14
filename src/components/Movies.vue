<template>
  <div class="container">
    <div class="search_input">
      <SearchInput @mySearch="searchMovie"/>
    </div>
    <div class="movies_list">
        <StarWars v-for="(film, index) in filteredDetailsStarWars" :key="index" :itemStarWars="film" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import StarWars from './StarWars.vue';
import SearchInput from './SearchInput.vue';

export default {
  name: 'MoviesFilm',

  components: {
    StarWars,
    SearchInput,
  },
  
  data(){
      return {
          apiUrlStarWars: "https://api.themoviedb.org/3/search/movie?api_key=4f0618c8f1e9a235de03917262238b33&query=star+wars",
          detailsStarWars: [],
          userText: "",
      }
  },

  created(){
    axios.get(this.apiUrlStarWars)
    .then(result => {
        this.detailsStarWars = result.data.results;
        console.log(this.detailsStarWars);  
        console.log(result.data);  
    }).catch(error => {
        console.log("Error", error);
    })
  },

  methods: {
    searchMovie(textUser){
       this.userText = textUser;
       console.log(textUser);
    }
  },

  computed: {
    filteredDetailsStarWars (){
      if (this.userText === ""){
        return this.detailsStarWars
      } else {
        return this.detailsStarWars.filter(item => {
        return item.original_title.toLowerCase().includes(this.userText.toLowerCase())
      })
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  .container {
    background-color: rgb(33, 39, 65);
    padding-top: 40px;
    padding-bottom: 20px;
  }

  .search_input {
    text-align: center;
  }
  .movies_list {
    width: 80%;
    display: flex;
    flex-wrap: wrap;
    margin: auto;
    color: white;
  }

</style>
