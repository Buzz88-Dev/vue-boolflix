<template>
  <div class="card"> 
    <!-- <img :src="itemLordOfTheRings.poster_path" :alt="itemLordOfTheRings.original_title"> -->
    <div class="text">
      <h3>Titolo Originale: {{ itemLordOfTheRings.original_title }}</h3>
      <h3>Titolo: {{ itemLordOfTheRings.title }}</h3>
      <h3>Voto: {{itemLordOfTheRings.vote_average}}</h3>
      <h3>Lingua originale: {{itemLordOfTheRings.original_language}}</h3>
      <!-- <p>{{itemLordOfTheRings.overview}}</p> -->
    </div> 											
  </div>
</template>

<script>
export default {
  name: 'TheLordOfTheRings',

  props: {
      itemLordOfTheRings: Object
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  .card {
    width: calc((100% /4) - 40px);
    margin: 0  20px 0px 20px;
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
