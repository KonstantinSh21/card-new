<template>

<div>

      <Wrapper class="wrapper"
      v-if='closeWrapperBoolean' 
      v-bind:closeWrapperBoolean='closeWrapperBoolean'


      v-on:closeWrapper='closeWrapper'

 />




<!-- Другой элемент -->

<div 
    class='wrapper'
    v-else-if="closeWrapperBooleanFinall">


      <h3 class="points">
          {{points}} Очков
      </h3>



      <div class='wrapper-cards'>

      
        
          <Game
              class='cards'

              v-bind:key='card'
              v-bind:cards="cards"
              v-bind:card='card'
              v-for='card in cards'
              v-bind:keyCard='card.id' 
              v-bind:cardsTitle="cards.title"

              v-on:coup='coup'
        />
 
          
        
     
        
      </div>



  


      <button 
      class="button"
      v-bind:closeWrapperBooleanFinall="closeWrapperBooleanFinall == true"
      v-on:click='close'>

      Завершить игру

      </button>


</div>



<!-- Другой элемент -->
 <WrapperFinal 
  v-bind:points='points'
  v-on:closeFinal='closeFinal'
  v-else
  />



</div>  


</template>

<script>
import Game from './components/Game.vue'
import Wrapper from './components/Wrapper.vue'
import WrapperFinal from './components/WrapperFinal.vue'



class Check{
    
    constructor(card, compArray, data, points) {


    compArray.push(card)

      if(compArray.length === 2){
        

        let idOne = compArray[0].id
        let keyOne = compArray[0].keyCard
        let idTwo = compArray[1].id
        let keyTwo = compArray[1].keyCard

        if(idOne > idTwo){
          idOne = compArray[1].id
          idTwo = compArray[0].id
        }




        // если пытаемся перевернуть туже карту что и нажули первый раз
        if(idOne == idTwo){


          data.cards[idOne - 1 ].completed = true
          compArray.pop()
         }

            // Тут удаляем два элемента из массива 
          else if(idOne !== idTwo && keyOne == keyTwo){

            const before = data.cards.slice(0, idOne - 1)
            const meddle = data.cards.slice(idOne , idTwo - 1)
            const after = data.cards.slice(idTwo)

            // создаем новый массив без двух одинаковых карт
            let newArray = [...before,...meddle, ...after]
            

          // Вместо старых карт теперь вставляется платка на всегда чтобы ничего не ломалось
        
          data.cards[idOne -1].nativeTitle = data.cards[idOne -1].title = data.cards[idOne-1].titleNon = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'
          data.cards[idTwo -1].nativeTitle = data.cards[idTwo -1].title = data.cards[idTwo-1].titleNon = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'
             
             
          


            // считаем количество очков 
            let newPoinst = points + newArray.length

            
            data.points = newPoinst
            


            // обновляет массивы 
            newArray = []
            data.compArray = []
         } 
          
          // если небходимо перевернуть карты обратно обратно все 
          else if(keyOne == keyTwo ||
              idOne !== idTwo || keyOne !== keyTwo || keyOne !== keyTwo
            ){

        
          // Даю значения картам чтобы они закрылись 
           
          data.cards[idOne - 1 ].completed = false
          data.cards[idTwo - 1].completed = false


          // Сравнивает состояние и дает свои значения 
          if(data.cards[idOne - 1 ].completed == false){
            data.cards[idOne - 1 ].title = data.cards[idOne - 1 ].titleNon
          }
          if(data.cards[idTwo - 1 ].completed == false){
            data.cards[idTwo - 1 ].title = data.cards[idTwo - 1 ].titleNon
          }
             
                
            // нужно придумать как заставить false быть false


             
          // считаем баллы при не верном ответе
            const before = data.cards.slice(0, idOne - 1 )
            const meddle = data.cards.slice(idOne , idTwo - 1 )
            const after = data.cards.slice(idTwo)


            let newArray = [...before,...meddle, ...after]

              let newPoinstFail = points - newArray.length
              data.points = newPoinstFail

              // обновляем массив
              data.compArray = []
           }  

           // завершение игры
              if(
              data.cards[0].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[1].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[2].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[3].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[4].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[5].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[6].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[7].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[8].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC' &&
              data.cards[9].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[10].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[11].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[12].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[13].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[14].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[15].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[16].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'&&
              data.cards[17].title == 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAA1BMVEUAqEMucRsRAAAASElEQVR4nO3BgQAAAADDoPlTX+AIVQEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwDcaiAAFXD1ujAAAAAElFTkSuQmCC'
              ){
                data.closeWrapperBooleanFinall = !data.closeWrapperBooleanFinall
              }
             
        }
    }
}



export default {
  name: 'App',
  components: {
    Game, Wrapper, WrapperFinal
  },
    
   data() {
    return{
      
      cards:[
            {id: 1, keyCard: 1, nativeTitle: 'https://st.depositphotos.com/2127699/2238/i/450/depositphotos_22389095-stock-photo-playing-card-ace-of-hearts.jpg', title: 'https://st.depositphotos.com/2127699/2238/i/450/depositphotos_22389095-stock-photo-playing-card-ace-of-hearts.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false },
            {id: 2, keyCard: 2, nativeTitle: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/Knight_of_hearts_en.svg/1200px-Knight_of_hearts_en.svg.png', title: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/Knight_of_hearts_en.svg/1200px-Knight_of_hearts_en.svg.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 3, keyCard: 3, nativeTitle: 'https://c7.hotpng.com/preview/458/229/186/king-of-spades-playing-card-suit-jack-queen.jpg', title: 'https://c7.hotpng.com/preview/458/229/186/king-of-spades-playing-card-suit-jack-queen.jpg ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 4, keyCard: 4, nativeTitle: 'https://c7.hotpng.com/preview/658/413/96/poker-queen-of-spades-playing-card-card-game-queen.jpg ', title:'https://c7.hotpng.com/preview/658/413/96/poker-queen-of-spades-playing-card-card-game-queen.jpg ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 5, keyCard: 5, nativeTitle: 'https://astrometa.ru/images/winds/karty2/10-pik.png', title: 'https://astrometa.ru/images/winds/karty2/10-pik.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 6, keyCard: 6, nativeTitle: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D0%BB%D0%BE%D0%BF%D0%B0%D1%82-%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%B8%D0%B7%D0%BD%D0%B5-132808061.jpg', title: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D0%BB%D0%BE%D0%BF%D0%B0%D1%82-%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%B8%D0%B7%D0%BD%D0%B5-132808061.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 7, keyCard: 7, nativeTitle: 'https://astrometa.ru/images/winds/karty2/8-chervei.png', title: 'https://astrometa.ru/images/winds/karty2/8-chervei.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 8, keyCard: 8, nativeTitle: 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884174_960_720.png', title: 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884174_960_720.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 9, keyCard: 9, nativeTitle: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-%D1%81%D0%B5%D1%80%D0%B4%D0%B5%D1%86-%D0%BA%D0%BE%D1%81%D1%82%D1%8E%D0%BC-%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85-%D0%BA%D0%B0%D1%80%D1%82-142606432.jpg', title: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-%D1%81%D0%B5%D1%80%D0%B4%D0%B5%D1%86-%D0%BA%D0%BE%D1%81%D1%82%D1%8E%D0%BC-%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85-%D0%BA%D0%B0%D1%80%D1%82-142606432.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},


            {id: 10, keyCard: 1, nativeTitle: 'https://st.depositphotos.com/2127699/2238/i/450/depositphotos_22389095-stock-photo-playing-card-ace-of-hearts.jpg ', title: 'https://st.depositphotos.com/2127699/2238/i/450/depositphotos_22389095-stock-photo-playing-card-ace-of-hearts.jpg ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 11, keyCard: 2, nativeTitle:'https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/Knight_of_hearts_en.svg/1200px-Knight_of_hearts_en.svg.png', title: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/Knight_of_hearts_en.svg/1200px-Knight_of_hearts_en.svg.png ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 12, keyCard: 3, nativeTitle: 'https://c7.hotpng.com/preview/458/229/186/king-of-spades-playing-card-suit-jack-queen.jpg ', title: 'https://c7.hotpng.com/preview/458/229/186/king-of-spades-playing-card-suit-jack-queen.jpg ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 13, keyCard: 4, nativeTitle:'https://c7.hotpng.com/preview/658/413/96/poker-queen-of-spades-playing-card-card-game-queen.jpg ', title: 'https://c7.hotpng.com/preview/658/413/96/poker-queen-of-spades-playing-card-card-game-queen.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 14, keyCard: 5, nativeTitle: 'https://astrometa.ru/images/winds/karty2/10-pik.png', title: 'https://astrometa.ru/images/winds/karty2/10-pik.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 15, keyCard: 6, nativeTitle: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D0%BB%D0%BE%D0%BF%D0%B0%D1%82-%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%B8%D0%B7%D0%BD%D0%B5-132808061.jpg', title: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D0%BB%D0%BE%D0%BF%D0%B0%D1%82-%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%B8%D0%B7%D0%BD%D0%B5-132808061.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 16, keyCard: 7, nativeTitle: 'https://astrometa.ru/images/winds/karty2/8-chervei.png', title: 'https://astrometa.ru/images/winds/karty2/8-chervei.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 17, keyCard: 8, nativeTitle: 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884174_960_720.png', title: 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884174_960_720.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 18, keyCard: 9, nativeTitle: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-%D1%81%D0%B5%D1%80%D0%B4%D0%B5%D1%86-%D0%BA%D0%BE%D1%81%D1%82%D1%8E%D0%BC-%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85-%D0%BA%D0%B0%D1%80%D1%82-142606432.jpg', title: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-%D1%81%D0%B5%D1%80%D0%B4%D0%B5%D1%86-%D0%BA%D0%BE%D1%81%D1%82%D1%8E%D0%BC-%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85-%D0%BA%D0%B0%D1%80%D1%82-142606432.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
          ],


       compArray:[],
       points: 0, 
       closeWrapperBoolean: true,
       closeWrapperBooleanFinall: true, 

       
     }
   },

   
    

    

methods: {

  closeWrapper(){
//Закрывает первый компонент открывает второй
 this.closeWrapperBoolean = !this.closeWrapperBoolean


// Созадает задержку чтобы карты перевернулись на 5 секунд перед игрой
    setTimeout(() => {
       for(let i = 0; i < this.cards.length; i++){

        
          this.cards[i].open = false
        
        if (this.cards[i].open == true){
            this.cards[i].title = this.cards[i].nativeTitle
        } else (this.cards[i].title = this.cards[i].titleNon)  
      } 
    }, 5000)  
  },


// Закрываем игральное окно и переходим к последнему элементу
  close(){
    
     this.closeWrapperBooleanFinall = !this.closeWrapperBooleanFinall
  },


  // Закрвываем последнее окно обновляем все данные и начинаем сначала
  closeFinal(){
    this.closeWrapperBoolean = !this.closeWrapperBoolean
    this.closeWrapperBooleanFinall = !this.closeWrapperBooleanFinall

    //Рандомно раскидываю массив
    let oldArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18]

    
    let count = 0;
    function compareRandom() {
      count++;
      return Math.random() - 0.5;
    }
    oldArray.sort(compareRandom);
    


    let oldCardsArray= [
            {id: 1, keyCard: 1, nativeTitle: 'https://st.depositphotos.com/2127699/2238/i/450/depositphotos_22389095-stock-photo-playing-card-ace-of-hearts.jpg', title: 'https://st.depositphotos.com/2127699/2238/i/450/depositphotos_22389095-stock-photo-playing-card-ace-of-hearts.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false },
            {id: 2, keyCard: 2, nativeTitle: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/Knight_of_hearts_en.svg/1200px-Knight_of_hearts_en.svg.png', title: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/Knight_of_hearts_en.svg/1200px-Knight_of_hearts_en.svg.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 3, keyCard: 3, nativeTitle: 'https://c7.hotpng.com/preview/458/229/186/king-of-spades-playing-card-suit-jack-queen.jpg', title: 'https://c7.hotpng.com/preview/458/229/186/king-of-spades-playing-card-suit-jack-queen.jpg ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 4, keyCard: 4, nativeTitle: 'https://c7.hotpng.com/preview/658/413/96/poker-queen-of-spades-playing-card-card-game-queen.jpg ', title:'https://c7.hotpng.com/preview/658/413/96/poker-queen-of-spades-playing-card-card-game-queen.jpg ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 5, keyCard: 5, nativeTitle: 'https://astrometa.ru/images/winds/karty2/10-pik.png', title: 'https://astrometa.ru/images/winds/karty2/10-pik.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 6, keyCard: 6, nativeTitle: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D0%BB%D0%BE%D0%BF%D0%B0%D1%82-%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%B8%D0%B7%D0%BD%D0%B5-132808061.jpg', title: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D0%BB%D0%BE%D0%BF%D0%B0%D1%82-%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%B8%D0%B7%D0%BD%D0%B5-132808061.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 7, keyCard: 7, nativeTitle: 'https://astrometa.ru/images/winds/karty2/8-chervei.png', title: 'https://astrometa.ru/images/winds/karty2/8-chervei.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 8, keyCard: 8, nativeTitle: 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884174_960_720.png', title: 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884174_960_720.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 9, keyCard: 9, nativeTitle: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-%D1%81%D0%B5%D1%80%D0%B4%D0%B5%D1%86-%D0%BA%D0%BE%D1%81%D1%82%D1%8E%D0%BC-%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85-%D0%BA%D0%B0%D1%80%D1%82-142606432.jpg', title: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-%D1%81%D0%B5%D1%80%D0%B4%D0%B5%D1%86-%D0%BA%D0%BE%D1%81%D1%82%D1%8E%D0%BC-%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85-%D0%BA%D0%B0%D1%80%D1%82-142606432.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},


            {id: 10,keyCard: 1, nativeTitle: 'https://st.depositphotos.com/2127699/2238/i/450/depositphotos_22389095-stock-photo-playing-card-ace-of-hearts.jpg ', title: 'https://st.depositphotos.com/2127699/2238/i/450/depositphotos_22389095-stock-photo-playing-card-ace-of-hearts.jpg ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 11, keyCard: 2, nativeTitle:'https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/Knight_of_hearts_en.svg/1200px-Knight_of_hearts_en.svg.png', title: 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/dc/Knight_of_hearts_en.svg/1200px-Knight_of_hearts_en.svg.png ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 12, keyCard: 3, nativeTitle: 'https://c7.hotpng.com/preview/458/229/186/king-of-spades-playing-card-suit-jack-queen.jpg ', title: 'https://c7.hotpng.com/preview/458/229/186/king-of-spades-playing-card-suit-jack-queen.jpg ', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 13, keyCard: 4, nativeTitle:'https://c7.hotpng.com/preview/658/413/96/poker-queen-of-spades-playing-card-card-game-queen.jpg ', title: 'https://c7.hotpng.com/preview/658/413/96/poker-queen-of-spades-playing-card-card-game-queen.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 14, keyCard: 5, nativeTitle: 'https://astrometa.ru/images/winds/karty2/10-pik.png', title: 'https://astrometa.ru/images/winds/karty2/10-pik.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 15, keyCard: 6, nativeTitle: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D0%BB%D0%BE%D0%BF%D0%B0%D1%82-%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%B8%D0%B7%D0%BD%D0%B5-132808061.jpg', title: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F-%D0%BA%D0%B0%D1%80%D1%82%D0%B0-%D0%BB%D0%BE%D0%BF%D0%B0%D1%82-%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BD%D0%B0-%D0%B1%D0%B5%D0%BB%D0%B8%D0%B7%D0%BD%D0%B5-132808061.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 16, keyCard: 7, nativeTitle: 'https://astrometa.ru/images/winds/karty2/8-chervei.png', title: 'https://astrometa.ru/images/winds/karty2/8-chervei.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 17, keyCard: 8, nativeTitle: 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884174_960_720.png', title: 'https://cdn.pixabay.com/photo/2015/08/11/11/56/spades-884174_960_720.png', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
            {id: 18, keyCard: 9, nativeTitle: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-%D1%81%D0%B5%D1%80%D0%B4%D0%B5%D1%86-%D0%BA%D0%BE%D1%81%D1%82%D1%8E%D0%BC-%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85-%D0%BA%D0%B0%D1%80%D1%82-142606432.jpg', title: 'https://thumbs.dreamstime.com/b/%D0%B8%D0%B3%D1%80%D0%B0-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-%D1%81%D0%B5%D1%80%D0%B4%D0%B5%D1%86-%D0%BA%D0%BE%D1%81%D1%82%D1%8E%D0%BC-%D0%B8%D0%B3%D1%80%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85-%D0%BA%D0%B0%D1%80%D1%82-142606432.jpg', titleNon: 'https://i.pinimg.com/originals/b1/51/b4/b151b48f2d77cdd03b17256ce25886a5.jpg', completed: false, open: false},
          ]
    
    //Союираю новый state с рандомными данными
    this.cards = [
          {id: 1, keyCard: oldCardsArray[oldArray[0] -1].keyCard, nativeTitle:oldCardsArray[oldArray[0] -1].nativeTitle, title: oldCardsArray[oldArray[0] -1].title , titleNon: oldCardsArray[oldArray[0] -1].titleNon , completed: false, open: false},
          {id: 2, keyCard: oldCardsArray[oldArray[1] -1].keyCard, nativeTitle: oldCardsArray[oldArray[1] -1].nativeTitle, title: oldCardsArray[oldArray[1] -1].title , titleNon: oldCardsArray[oldArray[1] -1].titleNon , completed: false, open: false},
          {id: 3, keyCard: oldCardsArray[oldArray[2] -1].keyCard, nativeTitle: oldCardsArray[oldArray[2] -1].nativeTitle, title: oldCardsArray[oldArray[2] -1].title , titleNon: oldCardsArray[oldArray[2] -1].titleNon , completed: false, open: false},
          {id: 4, keyCard: oldCardsArray[oldArray[3] -1].keyCard, nativeTitle: oldCardsArray[oldArray[3] -1].nativeTitle, title: oldCardsArray[oldArray[3] -1].title , titleNon: oldCardsArray[oldArray[3] -1].titleNon , completed: false, open: false},
          {id: 5, keyCard: oldCardsArray[oldArray[4] -1].keyCard, nativeTitle: oldCardsArray[oldArray[4] -1].nativeTitle, title: oldCardsArray[oldArray[4] -1].title , titleNon: oldCardsArray[oldArray[4] -1].titleNon , completed: false, open: false},
          {id: 6, keyCard: oldCardsArray[oldArray[5] -1].keyCard, nativeTitle: oldCardsArray[oldArray[5] -1].nativeTitle, title: oldCardsArray[oldArray[5] -1].title , titleNon: oldCardsArray[oldArray[5] -1].titleNon , completed: false, open: false},
          {id: 7, keyCard: oldCardsArray[oldArray[6] -1].keyCard, nativeTitle: oldCardsArray[oldArray[6] -1].nativeTitle, title: oldCardsArray[oldArray[6] -1].title , titleNon: oldCardsArray[oldArray[6] -1].titleNon , completed: false, open: false},
          {id: 8, keyCard: oldCardsArray[oldArray[7] -1].keyCard, nativeTitle: oldCardsArray[oldArray[7] -1].nativeTitle, title: oldCardsArray[oldArray[7] -1].title , titleNon: oldCardsArray[oldArray[7] -1].titleNon , completed: false, open: false},
          {id: 9, keyCard: oldCardsArray[oldArray[8] -1].keyCard, nativeTitle: oldCardsArray[oldArray[8] -1].nativeTitle, title: oldCardsArray[oldArray[8] -1].title , titleNon: oldCardsArray[oldArray[8] -1].titleNon , completed: false, open: false},
          {id: 10, keyCard: oldCardsArray[oldArray[9] -1].keyCard, nativeTitle: oldCardsArray[oldArray[9]-1].nativeTitle, title: oldCardsArray[oldArray[9] -1].title , titleNon: oldCardsArray[oldArray[9] -1].titleNon , completed: false, open: false},
          {id: 11, keyCard: oldCardsArray[oldArray[10] -1].keyCard, nativeTitle: oldCardsArray[oldArray[10] -1].nativeTitle, title : oldCardsArray[oldArray[10] -1].title , titleNon: oldCardsArray[oldArray[10] -1].titleNon , completed: false, open: false},
          {id: 12, keyCard: oldCardsArray[oldArray[11] -1].keyCard, nativeTitle: oldCardsArray[oldArray[11] -1].nativeTitle, title : oldCardsArray[oldArray[11] -1].title , titleNon: oldCardsArray[oldArray[11] -1].titleNon , completed: false, open: false},
          {id: 13, keyCard: oldCardsArray[oldArray[12] -1].keyCard, nativeTitle: oldCardsArray[oldArray[12] -1].nativeTitle, title : oldCardsArray[oldArray[12] -1].title , titleNon: oldCardsArray[oldArray[12] -1].titleNon , completed: false, open: false},
          {id: 14, keyCard: oldCardsArray[oldArray[13] -1].keyCard, nativeTitle: oldCardsArray[oldArray[13] -1].nativeTitle, title : oldCardsArray[oldArray[13] -1].title , titleNon: oldCardsArray[oldArray[13] -1].titleNon , completed: false, open: false},
          {id: 15, keyCard: oldCardsArray[oldArray[14] -1].keyCard, nativeTitle: oldCardsArray[oldArray[14] -1].nativeTitle, title : oldCardsArray[oldArray[14] -1].title , titleNon: oldCardsArray[oldArray[14] -1].titleNon , completed: false, open: false},
          {id: 16, keyCard: oldCardsArray[oldArray[15] -1].keyCard, nativeTitle: oldCardsArray[oldArray[15] -1].nativeTitle, title : oldCardsArray[oldArray[15] -1].title , titleNon: oldCardsArray[oldArray[15] -1].titleNon , completed: false, open: false},
          {id: 17, keyCard: oldCardsArray[oldArray[16] -1].keyCard, nativeTitle: oldCardsArray[oldArray[16] -1].nativeTitle, title : oldCardsArray[oldArray[16] -1].title , titleNon: oldCardsArray[oldArray[16] -1].titleNon , completed: false, open: false},
          {id: 18, keyCard: oldCardsArray[oldArray[17] -1].keyCard, nativeTitle: oldCardsArray[oldArray[17] -1].nativeTitle, title : oldCardsArray[oldArray[17] -1].title , titleNon: oldCardsArray[oldArray[17] -1].titleNon , completed: false, open: false},
      ]
      
     this.points = 0
       

  },

     
// переворачивает карты 
   coup(id, keyCard, card ) {
 

// меняет false на tpy и сравнивает дает им свои значения 
        let a = id - 1
        
        
         this.cards[a].completed = !this.cards[a].completed
        

        
        
        if (this.cards[a].completed == true){
            this.cards[a].title = this.cards[a].nativeTitle
        } else(this.cards[a].title = this.cards[a].titleNon)
       
          // создается задержка чтобы успеть посмотерть что за карта находить
          // также метод check делает различные манипуляции с data (удаляет элементы из дома, переворачивает и т.д)
        setTimeout(() => {
            new Check(card, this.compArray, this, this.points)
        }, 500)

        

       },

    }

}
  

</script>

<style scoped>
  *{
    padding: 0px;
    margin: 0px;
  }



  .points{
    text-align: right;
    color: #e8fc32;
    margin-right: 100px;
  }
  .wrapper{
    margin: 0 auto;
    text-align: center;
    background: #00A843;
    width: 100vw;
    height: 100vh;    
    padding-bottom: 900px;
}

.wrapper-cards{
  
  width: 70%;
  margin: 0 auto;
}

.cards{
  display: inline;
}

@media screen and (max-width: 1253px) {
    .wrapper-cards{
      width: 70%;
      

    }
}

@media screen and (max-width: 1200px) {
    .wrapper-cards{
      width: 40%;

    }
}



.button{
 
  margin: 0 auto;
  background-color: #12CDD4;
  color: #fff;
  font-size: 20px;
  width: 300px;
  height: 60px;
  border-radius: 100px;

}


</style>
