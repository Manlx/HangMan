<template>
  <div class="holder">
    <h1>Number of letters: {{CurrentValue}}</h1>
    <input type="range" :min="this.Min" :max="this.Max" v-model="this.CurrentValue" class="slider" id="myRange" @change="ValueChanged">
    
  </div>
</template>

<script>
export default {
    props:["Max","Min","Value"],
    data:function(){
        return {CurrentValue:0}
    },
    methods:{
      ValueChanged:function(){
        this.$emit("ValueChange",this.CurrentValue);
      },
      // sayHigh:function(){
      //   alert("Hi")
      // },
      helloWorld:function(){
        alert("Hello World")
      }
    },
    created:function(){
        this.CurrentValue = this.Value
    },
    
}
</script>

<style scoped>
    .holder{
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
        flex-direction: column;
        margin-top: 2vh;
    }

    .slidecontainer {
        width: 100%;
    }

.slider {
  -webkit-appearance: none;
  width: 30%;
  height: 25px;
  background: #565656;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: .2s;
  border-radius: 10px;
}

.slider:hover {
  opacity: 1;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 25px;
  height: 25px;
  background: green;
  cursor: pointer;
  border-radius: 10px;
}

.slider::-moz-range-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 25px;
  height: 25px;
  background: green;
  cursor: pointer;
  border-radius: 10px;
}
h1{
  margin: 0 0 1vh 0;
}
</style>