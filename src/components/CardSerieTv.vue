<template>
  <div class="card"> 
    <img :src="pathimmagineFilm + itemSerieTV.poster_path" :alt="itemSerieTV.original_title">
    <div class="text">
      <h3>Titolo Originale: {{ itemSerieTV.original_title }}</h3>
      <h3>Titolo: {{ itemSerieTV.title }}</h3>
      <h3>Voto: {{itemSerieTV.vote_average}}</h3>
      <div class="language">
          <h3>Lingua originale: {{itemSerieTV.original_language}}</h3>
          <img :src="flags(this.itemSerieTV.original_language)">
      </div>
    </div> 											
  </div>
</template>

<script>
export default {
  name: 'CardSerieTv',

  data() {
    return {
      pathimmagineFilm : "https://image.tmdb.org/t/p/w342",
    }
  },

  props: {
      itemSerieTV: Object
  },

  methods: {
    flags(lingua){
      if (lingua === "es" || lingua === "it" || lingua === "es" || lingua === "en" || lingua === "ja") {
        return require('../assets/flag/' + lingua + ".png")
      } else {
        return require('../assets/flag/vuota.png')
      }
    }
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

    .language {
      display: flex;

      img {
        width: 10%;
      }
    }
  }
</style>