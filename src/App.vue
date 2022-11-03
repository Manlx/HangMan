<template>
  <div class="">
    <word-display :displayWord="this.DisplayingWord" />
    <!-- <word-display -->
    <div class="flexCenter">
      <div class="hangManImage">

      </div>
      <div class="ButtonGrid">
        <div v-for="value,index in this.Alpha" :key="index" class="flexCenter">
          <key-button  :ButtonDisplay="value" @Clicked="ButtonClicked"/>
        </div>
      </div>
    </div>
  </div>
    
</template>

<script>

import KeyButton from './components/KeyButton.vue'
import WordDisplay from './components/WordDisplay.vue'
export default{
  name: "App",
  components: { KeyButton, WordDisplay },
  data:function(){
    return {
        Alpha: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split(""),
        DisplayingWord:""
    }
  },
  methods:{
    ButtonClicked:function(Char){
      this.DisplayingWord += Char;
    }
  }
}
</script>
  
<style>
  .hangManImage{
    display: flex;
    width: 30%;
    aspect-ratio: 1/1;
    margin: 1% 5%;
    background-image: url('https://static.vecteezy.com/packs/media/vectors/term-bg-1-666de2d9.jpg');
    background-position: center;
    background-size: 100% 100%;
    background-color: #565656;

    border-radius: 20px;
  }

  .ButtonGrid{
    /* background-color: firebrick; */
    width: 60%;
    display: grid;
    grid-template-columns: repeat(9,1fr) ;
    column-gap: 20px;
    row-gap: 20px;
    margin: 5%;
  }

  .flexCenter{
    display: flex;
    justify-content: center;
    align-items: center;
  }

  *{
    margin: 0;
    padding: 0;
  }

  body{
    background: #232323;
  }
</style>
