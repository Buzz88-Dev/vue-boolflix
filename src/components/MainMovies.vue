<template>
  <div class="container">
    <div class="search_input">
      <SearchInput @mySearch="searchMovie"/>
    </div>
    <div class="movies_list">
        <CardFilm v-for="(film, index) in detailsMovies" :key="index" :itemFilm="film" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CardFilm from './CardFilm.vue';
import SearchInput from './SearchInput.vue';

export default {
  name: 'MoviesFilm',

  components: {
    CardFilm,
    SearchInput,
  },
  
  data(){
      return {
          apiUrlMovies: "https://api.themoviedb.org/3/search/movie?api_key=049b0824b24d9a73de8047a8a18e7c77&language=it-IT",
          detailsMovies: [],
          userText: "",
      }
  },

  created(){
    this.getListMovies()
  },

  methods: {

    getListMovies(){
      if (this.userText !== ""){
          let currentApiUrl = this.apiUrlMovies + "&query=" + this.userText;
          console.log(currentApiUrl);
          axios.get(currentApiUrl)
          .then(result => {
            this.detailsMovies = result.data.results;
            console.log(this.detailsMovies);    
          }).catch(error => {
          console.log("Error", error);
          })
        } 
    },

    searchMovie(userInput){
       this.userText = userInput;
       console.log(this.userText);
       this.getListMovies();
    }
  },

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
