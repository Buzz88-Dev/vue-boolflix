<template>
  <div class="discs_list">
            <TheLordOfTheRings v-for="(film, index) in detailsTheLordOfTheRings" :key="index" :itemLordOfTheRings="film" />
     </div>
</template>

<script>
import axios from "axios";
import TheLordOfTheRings from './TheLordOfTheRings.vue';

export default {
  name: 'MoviesFilm',

  components: {
    TheLordOfTheRings,
  },
  
  data(){
      return {
          apiUrlTheLordOfTheRings: "https://api.themoviedb.org/3/search/movie?api_key=4f0618c8f1e9a235de03917262238b33&query=il+signore+degli+anelli",
          detailsTheLordOfTheRings: [],
      }
  },

  created(){
    axios.get(this.apiUrlTheLordOfTheRings)
    		.then(result => {
            this.detailsTheLordOfTheRings = result.data.results;
        		console.log(this.detailsTheLordOfTheRings);    
    		}).catch(error => {
        console.log("Error", error);
    	})
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
