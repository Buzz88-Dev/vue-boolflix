<template>
  <div>
    <div class="search_input">
      <HeaderInput @mySearch="searchMovie"/>
    </div>

    <div class="container_main">
      <h2>Tutti i FILM e le SERIE che vuoi su BOOLFIX</h2>
      <div v-if="userText !== ''">
          <div class="movies_list">
            <CardFilm v-for="(film) in detailsMovies" :key="film.id" :itemFilm="film" />
          </div>
          <div class="serieTV_list">
            <CardSerieTv v-for="(serieTV) in detailsSerieTV" :key="serieTV.id" :itemSerieTV="serieTV" />
          </div>
      </div>
      <div v-else>
          <div class="movies_list">
            <CardFilm v-for="(film) in movies" :key="film.id" :itemFilm="film" />
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CardFilm from './CardFilm.vue';
import CardSerieTv from './CardSerieTv.vue';
import HeaderInput from './Header.vue';

export default {
  name: 'MoviesFilm',

  components: {
    CardFilm,
    HeaderInput,
    CardSerieTv,
  },
  
  data(){
      return {
          apiUrlMovies: "https://api.themoviedb.org/3/search/movie?api_key=049b0824b24d9a73de8047a8a18e7c77&language=it-IT",
          apiUrlSerieTV: "https://api.themoviedb.org/3/search/tv?api_key=049b0824b24d9a73de8047a8a18e7c77&language=it_IT", 
          detailsMovies: [],
          detailsSerieTV: [],
          movies: [],
          userText: "",
          originalLanguagesArray: [],
          votesArray: [],
          listFilm: [],
      }
  },

  created(){
    this.getListMovies(),
    this.getListSerieTV(),
    this.searchOriginalLanguage(),
    this.searchVotes(),
    this.getSchermata()
  },

  methods: {

    getSchermata(){
      let listaPrincipale = this.apiUrlMovies + "&query=the";
      console.log(listaPrincipale);
      axios.get(listaPrincipale)
      .then((result) => {
        this.movies = result.data.results;
        console.log(this.movies)
      }).catch((error) => {
        console.log("Errore", error);
      })
    },

    getListMovies(){
      if (this.userText !== ""){
          let currentApiUrlMovies = this.apiUrlMovies + "&query=" + this.userText;
          console.log(currentApiUrlMovies);

          axios.get(currentApiUrlMovies)
          .then(result => {
            this.detailsMovies = result.data.results;
            console.log(this.detailsMovies);
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
            // console.log(this.searchOriginalLanguage());
            this.searchVotes();
            // console.log(this.searchVotes());
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

    // mi creo una funzione solo per vedere quali sono le lingue che stampo
    searchOriginalLanguage(){
      this.detailsMovies.forEach(element => {
        if (!this.originalLanguagesArray.includes(element.original_language)){
          this.originalLanguagesArray.push(element.original_language);
        }
      });
      return this.originalLanguagesArray;
    },

    // mi creo una funzione solo per vedere i voti
    searchVotes(){
      this.detailsMovies.forEach(element => {
        if (!this.votesArray.includes(element.vote_average)){
          this.votesArray.push(element.vote_average);
        }
      });
      return this.votesArray;
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  .search_input {
    background-color: black;
  }

  .container_main {
    padding: 40px 0px;
    background-color: rgb(86, 84, 84);
    height: calc(100vh - 100px);
    overflow-y: scroll;

    h2 {
      text-align: center;
      color: black;
    }


    .movies_list, .serieTV_list {
    width: 90%;
    margin: auto;
    display: flex;
    flex-wrap: wrap;
    }

    .card {
    width: calc((100% / 4) - 20px);

    margin: 40px 10px;

      img {
        width: 100%;
        height: 100%;
      }
    } 
  }

</style>
