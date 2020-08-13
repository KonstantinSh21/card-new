<template>
<div >

        <img
        v-bind:src="card.title"
        class="wrapper-card"
        v-on:click="$emit('coup', card.id, card.keyCard, card)">
    

  </div>


</template>

<script>
export default {
  name: 'Game',
  props: ['cards', 'id', 'card', 'cardsTitle'],



  }

</script>


<style scoped>


.wrapper-card{
  display: inline-block;
  width: 120px;
  height: 160px;
  margin: 10px;
}





</style>
