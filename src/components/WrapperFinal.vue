<template>
  <div class="wrapper">
      <div class="game">
          Игра завершина!
      </div>

      <img 
      src="https://i.ytimg.com/vi/SPezfzQm80Y/maxresdefault.jpg"
      class="imgFinal"

      />

      <div class="points">
        Вы набрали {{points}} баллов
      </div>
      
      <button
      class="button" 
      v-on:click='$emit("closeFinal")'>
          Повторить игру
      </button>
  </div>
</template>

<script>
export default {
    name: 'WrapperFinal',
    props:['points'],
       
     
    
    
}
</script>

<style scoped>
    *{
        padding: 0px;
        margin: 0px;
    }

    .wrapper{
    margin: 0 auto;
    text-align: center;
    background: #368C4A;
    width: 100vw;
    height: 100vh;
    }
    .imgFinal{
        padding-top: 60px;
        height: 100px;
    }

    .game{
        padding-top: 50px;
        color: #ffffff;
        font-size: 50px;
    }

    .points{
        padding-top: 50px;
        color: #ffffff;
        font-size: 25px;
    }

    .button{
  margin-top: 10px;
  margin: 0 auto;
  background-color: #12CDD4;
  color: #fff;
  font-size: 20px;
  width: 300px;
  height: 60px;
  border-radius: 100px;
    }
</style>