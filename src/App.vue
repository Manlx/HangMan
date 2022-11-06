<template>
  <div class="MainAppArea">
    <div v-if="!this.gameOver">
      <word-length-comp  :ref="`myChild`" :Max="this.WLMax" :Min="this.WLMin" :Value="this.WLStartValue" @ValueChange="this.rangeChange"/>
      <word-display :displayWord="this.DisplayingWord" />
      <div class="flexCenter">
        <hang-man-image :DisplayText="`Lives Remaining: ${this.LivesRemaining}`" :dispImage="`./resources/images/${this.DisplayImageUrl}`" />
        <div class="ButtonGrid">
          <div v-for="value,index in this.Alpha" :key="index" class="flexCenter">
            <key-button :ref="`BD`" :ID="index" :ButtonDisplay="value" @clicked="ButtonClicked" />
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <game-over-screen :DisplayMessage="this.gameOverMessage" @PlayAgain="playAgainClicked"/>
    </div>
  </div>
</template>

<script>
const maxImages = 11;
console.log(maxImages)
function fillBlanks(char,blanks,answer){
  let Arr= blanks.split(" ")
  let Out = ""
  for (let i = 0; i < Arr.length;i++)
  {
    if (answer.charAt(i) == char)
    {
      Out += `${char} `
    }
    else{
      Out += `${Arr[i]} `
    }
  }
  return Out;
}

import KeyButton from './components/KeyButton.vue'
import WordDisplay from './components/WordDisplay.vue'
import WordLengthComp from './components/WordLengthComp.vue'
import HangManImage from './components/HangManImage.vue'
import GameOverScreen from './components/GameOverScreen.vue';

export default{
  name: "App",
  components: { KeyButton, WordDisplay, WordLengthComp, HangManImage, GameOverScreen },
  data:function(){
    return {
      Alpha: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split(""),
      DisplayingWord:"",
      AllWords:[],
      FilteredWords:[],
      WLStartValue:8,
      WLMin:3,
      WLMax:14,
      ChosenWord:"",
      LivesRemaining:5,
      Step:0,
      DisplayImageUrl:"0.png",
      DisplayStep: 0,
      gameOver:true,
      Winner:false,
      gameOverMessage:"Well done"
    }
  },
  methods:{
    ButtonClicked:function(Char,ID){
      this.$refs.BD[ID].correct = this.ChosenWord.includes(Char)
      if (this.$refs.BD[ID].correct)
      {
        this.DisplayingWord =  fillBlanks(Char,this.DisplayingWord,this.ChosenWord);
        if (!this.DisplayingWord.includes("_"))
        {
          this.gameOverMessage = "Well done :-}";
          this.gameOver = true;
        }
      }
      else
      {
        this.LivesRemaining--;
        this.DisplayStep += this.Step;
        if (this.DisplayStep > maxImages)
          this.DisplayStep = maxImages

        this.DisplayImageUrl = `${this.DisplayStep}.png`;
        if (this.LivesRemaining == 0)
        {
          this.gameOver = true;
          this.gameOverMessage = "oof Gett'em next time";
        }
          
      }
    },

    getWords:async function(){
      let response = await fetch("input.txt");
        
      if(response.status != 200) {
        throw new Error("Server Error");
      }
      let text_data = await response.text();
      text_data = text_data.split("\n")
      return text_data;
    },

    filterWords:function(e){
      this.FilteredWords = this.AllWords.filter(function(x){
        return x.length == e;
      })
    },

    generateDisplayWord:function(e){
      let temp = "";
      for (let i = 0; i < e;i++)
        temp += "_ ";
      this.DisplayingWord = temp;
    },

    rangeChange:function(e)
    {
      this.init(e);
    },

    init:function(WL)
    {
      let self = this;
      this.getWords().then(function(data){
        self.AllWords = data;
        self.filterWords(WL);
        self.generateDisplayWord(WL)
        self.ChosenWord = self.FilteredWords[Math.trunc(Math.random()*self.FilteredWords.length)].toUpperCase();
        self.Step = Math.trunc(maxImages/self.LivesRemaining);
        self.gameOver = false;
        console.log(self.ChosenWord)
      })
    },

    playAgainClicked:function(){
      this.init(this.WLStartValue);
    }
  },
  created:function(){
    this.init(this.WLStartValue);
  }
}
</script>
  
<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
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

  .MainAppArea{
    font-family: 'Roboto', sans-serif;
    color: white;
  }

  h1{
    font-size: 4rem;
  }

  .TopBar{
    display: flex;
    justify-content: space-around;
    align-content: center;
  }
</style>
