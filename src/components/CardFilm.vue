<template>
  <div class="card"> 
    <img :src="pathimmagineFilm + itemFilm.poster_path" :alt="itemFilm.original_title">
    <div class="text">
      <h3>Titolo Originale: {{ itemFilm.original_title }}</h3>
      <h3>Titolo: {{ itemFilm.title }}</h3>
      <h3>Voto: {{itemFilm.vote_average}}</h3>
      <h3>Lingua originale: {{itemFilm.original_language}}</h3>
    </div> 											
  </div>
</template>

<script>
export default {
  name: 'CardFilm',

  data() {
    return {
      pathimmagineFilm : "https://image.tmdb.org/t/p/w342",
    }
  },

  props: {
      itemFilm: Object
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
  }
</style>
