<template>
  <div class="holder">
    <div class="hangManImage" :style="{'background-image':`url('${this.dispImage}')`}">

    </div>
    <h1 class="TextDisplay">{{this.DisplayText}}</h1>
  </div>
</template>

<script>
export default {
    props:["DisplayText","dispImage"]
}
</script>

<style scoped>
  .hangManImage{
    display: flex;
    width: 30vw;
    aspect-ratio: 1/1;
    margin: 1% 5%;
    /* background-image: url('https://static.vecteezy.com/packs/media/vectors/term-bg-1-666de2d9.jpg'); */
    background-position: center;
    background-size: 90% 90%;
    background-color: #565656;
    background-repeat: no-repeat;
    border-radius: 20px;
  }

  .TextDisplay{
    /* margin: 1% 5%; */
    width: fit-content;
    transition: 1s;
    /* background-color: aqua; */
  }

  .holder{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 0 0 0 3vw;
  }
</style>