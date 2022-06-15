<template>
  <div class="card"> 
    <!-- <img :src="pathimmagineFilm + itemFilm.poster_path" :alt="itemFilm.original_title"> -->
    <img :src="pathimmagineFilm + itemFilm.backdrop_path" :alt="itemFilm.original_title">
    <div class="text">
      <h3>Titolo Originale: {{ itemFilm.original_title }}</h3>
      <h3>Titolo: {{ itemFilm.title }}</h3>
      <h3>Voto: {{itemFilm.vote_average}}</h3>
      <h3>Voto: {{vote(this.itemFilm.vote_average)}}</h3>
      <span >
            <!-- <font-awesome-icon v-for="(element, i) in vote()" :key="i+'n'" icon="fa-solid fa-star"/> -->
            <font-awesome-icon icon="far fa-star"/>
            <font-awesome-icon icon="fa-solid fa-user-secret" />
      </span>
      <div class="language">
          <h3>Lingua originale: {{itemFilm.original_language}}</h3>
          <img :src="flags(this.itemFilm.original_language)">
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
      voto: "",
      // star: '<font-awesome-icon icon="far fa-star" />',
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

    vote(votoAverage) {
        this.voto = Math.round(votoAverage / 2);
        console.log(this.voto);
        return this.voto
    },
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  .card {
    width: calc((100% /4) - 40px);
    margin: 0  20px 0px 20px;

    img {
      width: 100%;
      margin: auto;
    }
  }
  .text {
    display: flex;
    flex-direction: column;
    padding: 20px 0px;

    h3 {
      font-size: 12px;
      padding-top: 10px;
    }

    p {
      font-size: 10px;
    }

    span {
      color: white;
    }

    .language {
      display: flex;

      img {
        width: 10%;
      }
    }
  }
</style>
