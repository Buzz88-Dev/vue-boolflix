<template>
  <div class="container">
    <div class="search_input">
      <SearchInput @mySearch="searchMovie"/>
    </div>
    <div class="movies_list">
        <CardFilm v-for="(film, index) in detailsMovies" :key="index" :itemFilm="film" />
    </div>
    <div class="serieTV_list">
        <CardSerieTv v-for="(serieTV, i) in detailsSerieTV" :key="i" :itemSerieTV="serieTV" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CardFilm from './CardFilm.vue';
import CardSerieTv from './CardSerieTv.vue';

import SearchInput from './SearchInput.vue';

export default {
  name: 'MoviesFilm',

  components: {
    CardFilm,
    SearchInput,
    CardSerieTv,
  },
  
  data(){
      return {
          apiUrlMovies: "https://api.themoviedb.org/3/search/movie?api_key=049b0824b24d9a73de8047a8a18e7c77&language=it-IT",
          apiUrlSerieTV: "https://api.themoviedb.org/3/search/tv?api_key=049b0824b24d9a73de8047a8a18e7c77&language=it_IT",
          detailsMovies: [],
          detailsSerieTV: [],
          userText: "",
          originalLanguagesArray: [],
      }
  },

  created(){
    this.getListMovies(),
    this.getListSerieTV(),
    this.searchOriginalLanguage()
  },

  methods: {

    getListMovies(){
      if (this.userText !== ""){
          let currentApiUrlMovies = this.apiUrlMovies + "&query=" + this.userText;
          console.log(currentApiUrlMovies);

          axios.get(currentApiUrlMovies)
          .then(result => {
            this.detailsMovies = result.data.results;
            console.log(this.detailsMovies);
            this.searchOriginalLanguage();
            console.log(this.searchOriginalLanguage());
          }).catch(error => {
          console.log("Error", error);
          })
        } 
    },

    getListSerieTV(){
      if (this.userText !== ""){
          let currentApiUrlSerieTV = this.apiUrlSerieTV + "&query=" + this.userText;
          console.log(currentApiUrlSerieTV);

          axios.get(currentApiUrlSerieTV)
          .then(result => {
            this.detailsSerieTV = result.data.results;
            console.log(this.detailsSerieTV);
            this.searchOriginalLanguage();
            console.log(this.searchOriginalLanguage());
          }).catch(error => {
          console.log("Error", error);
          })
      } 
    },

    searchMovie(userInput){
       this.userText = userInput;
       console.log(this.userText);
       this.getListMovies();
       this.getListSerieTV();
    },

    searchOriginalLanguage(){
      this.detailsMovies.forEach(element => {
        if (!this.originalLanguagesArray.includes(element.original_language)){
          this.originalLanguagesArray.push(element.original_language);
        }
      });
      return this.originalLanguagesArray;
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
  .movies_list, .serieTV_list {
    width: 80%;
    display: flex;
    flex-wrap: wrap;
    margin: auto;
    color: white;
  }

</style>
