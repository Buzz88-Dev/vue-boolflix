<template>
  <div>
    <div class="card">    											
        <h3>{{ itemLordOfTheRings.original_title }}</h3>
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

</style>
