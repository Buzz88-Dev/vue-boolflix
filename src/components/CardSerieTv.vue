<template>
  <div class="card" v-on:mouseover="cardHover = true" v-on:mouseleave="cardHover = false"> 
    <div :class="cardHover ? 'd-none' : ''">
      <!-- <img :src="pathimmagineSerieTV + itemSerieTV.poster_path" :alt="itemSerieTV.original_title"> -->
      <img :src="pathimmagineSerieTV + itemSerieTV.poster_path" :alt="itemSerieTV.original_title">
    </div>
    
    <div class="text" :class="!cardHover ? 'd-none' : ''">

      <h6>Titolo Originale: {{ itemSerieTV.original_title }}</h6>
      <h5>Titolo: {{ itemSerieTV.title }}</h5>

      <span >
        <strong>Voto: </strong>
        <font-awesome-icon v-for="(element, i) in vote()" :key="i + 'y'" icon="fa-solid fa-star" />
        <font-awesome-icon v-for="(element, index) in noVote()" :key="index + 'x'" icon="far fa-star" />
         <!-- per evitare errori nella console aggiungo una stringa alla key -->
      </span>

      <h5 class="overview">Overview: {{ itemSerieTV.overview }}</h5>

      <div class="language">
        <h5>Lingua originale: </h5>
          <div class="language_image">
            <img :src="flags(this.itemSerieTV.original_language)">
          </div>  
      </div>
    </div> 											
  </div>
</template>

<script>
export default {
  name: 'CardSerieTv',

  data() {
    return {
      pathimmagineSerieTV : "https://image.tmdb.org/t/p/w342",
      votoSerieTV: "",
      cardHover: false,
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
    },

    vote() {
        this.votoSerieTV = Math.round(this.itemSerieTV.vote_average / 2);
        return this.votoSerieTV;
    },

    noVote(){
      return (5 - this.votoSerieTV);
    }
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
        padding: 20px 15px;
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