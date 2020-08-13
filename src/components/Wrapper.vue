<template>
  
<div class="wrapper">
      
          <img 
          src='https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg'
           alt="Карта">
          <h1> Игра "Memory" </h1>

      <button v-on:click="$emit('closeWrapper')">
          Начать игру
          
      </button>
  </div>
</template>

<script>
export default {
    props:['closeWrapperBoolean']
    

}
</script>

<style scoped>
.wrapper{
    background: #368C4A;
    width: 100vw;
    height: 100vh;
    margin-top: -28px;
    text-align: center;
    padding-bottom: 200px;    
}
h1, button{
    font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    position: relative;
    top: 120px;
    color: #fff;
}

img{
    position: relative;
    top: 60px;
    height: 200px;
}

button{
    margin-top: 10px;
    background-color: #12CDD4;
    color: #fff;
    font-size: 20px;
    width: 400px;
    height: 70px;
    border-radius: 100px;
}

button:hover{
    background-color: #17f4fc;
}
button:active{
    border: 1px solid #12CDD4;
    color: #696868;
}

/* адаптивка */
@media screen and (max-width: 600px) {
    img{
        position: relative;
        top: 80px;
        height: 150px;
    }
    h1{
        font-size: 25px;
    }

    button{
        margin-top: 20px;
        background-color: #12CDD4;
        color: #fff;
        font-size: 20px;
        width: 300px;
        height: 60px;
        border-radius: 100px;
}
}

</style>

</style>