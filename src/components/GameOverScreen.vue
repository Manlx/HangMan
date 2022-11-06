<template>
  <div class="main flexCenter">
    <div class="smallBlock flexCenter">
        <h1>{{this.DisplayMessage}}</h1>
        <button @click="clicked">Play Again</button>
    </div>
    
  </div>
</template>

<script>
export default {
    props:["DisplayMessage"],
    methods:{
        clicked:function(){
            this.$emit("PlayAgain");
        }
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
h1{
    font-family: 'Roboto', sans-serif;
    font-size: 4rem;
    transition: 1s;
}

.main{
    min-height: 100vh;
}

.smallBlock:hover h1{
    color: aqua;
}

.flexCenter{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.smallBlock{
    height: 75vh;
    width: 75vh;
    background-color: #454545;
    border-radius: 20px;
    justify-content: space-evenly;
}

button{
    padding: 4vh;
    background-color: cadetblue;
    border: none;
    margin: 10px;
    border-radius: 20px;
    font-family: 'Roboto', sans-serif;
    font-size: 4rem;
    transition: 1s;
    box-shadow: 0px 0px 10px 10px cadetblue;
    color: white;
    font-weight: bold;
}

button:hover{
    box-shadow: 0px 0px 7px 10px rgb(113, 255, 208);
    background-color: rgb(113, 255, 208);
    color: #232323;
}
</style>