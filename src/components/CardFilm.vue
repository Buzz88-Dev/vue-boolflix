<template>
  <div class="card" v-on:mouseover="cardHover = true" v-on:mouseleave="cardHover = false">
    <div :class="cardHover ? 'd-none' : ''">
      <img :src="pathimmagineFilm + itemFilm.poster_path" :alt="itemFilm.original_title">
    </div>
  
    <div class="text" :class="!cardHover ? 'd-none' : ''">

      <h6>Titolo Originale: {{ itemFilm.original_title }}</h6>
      <h5>Titolo: {{ itemFilm.title }}</h5>

      <span>
        <strong>Voto: </strong>
        <font-awesome-icon v-for="(element, i) in vote()" :key="i + 'n'" icon="fa-solid fa-star" />
        <font-awesome-icon v-for="(element, index) in noVote()" :key="index" icon="far fa-star" />
      </span>
  
      <h5 class="overview">Overview: {{ itemFilm.overview }}</h5>

      <div class="language">
        <h5>Lingua originale: </h5>
        <div class="language_image">
          <img :src="flags(this.itemFilm.original_language)">
        </div>       
      </div>

    </div> 											
  </div>
</template>

<script>
export default {
  name: 'CardFilm',

  data() {
    return {
      pathimmagineFilm : "https://image.tmdb.org/t/p/w342",
      votoFilm: "",
      cardHover: false,
    }
  },

  props: {
      itemFilm: Object,
  },

  methods: {
    flags(lingua){
      if (lingua === "es" || lingua === "it" || lingua === "es" || lingua === "fr" || lingua === "en" || lingua === "ja") {
        return require('../assets/flag/' + lingua + ".png")
      } else {
        return require('../assets/flag/vuota.png')
      }
      // oppure usare quest npmjs: https://www.npmjs.com/package/vue-lang-code-flags
    },

    vote() {
        this.votoFilm = Math.round(this.itemFilm.vote_average / 2);
        return this.votoFilm;
    },

    noVote(){
      return (5 - this.votoFilm);
    },

  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  .card {
    width: calc((100% / 4) - 20px);
    position: relative;
    background-color: black;
    margin: 40px 10px;

      img {
        width: 100%;
        height: 100%;
      }

      .text {
        position: absolute;
        display: flex;
        flex-direction: column;
        padding: 40px 15px;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        color: white;
        overflow-y: scroll; 

        .d-none {
          display: none;
        }


        h5, h6, strong {
          font-size: 15px;
        }

        h5 {
          margin: 5px 0px;
        }

        .language {
          display: flex;
          justify-content: flex-start;
          align-items: center;


          .language_image {
            width: 10%;
            height: auto;
            margin-left: 5px;
            font-size: 5px;
          }
        }
      }

  }

</style>
