<template>
    <div>
        <h1>{{this.displayWord}}</h1>
    </div>
  
</template>

<script>
export default {
    name:"WordDisplay",
    props:["displayWord"],
    methods:{
        
    }
}
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
    div{
        margin-top: 5vh;
        color: white;
        display: flex;
        justify-content: center;
        align-content: center;
        font-family: 'Roboto', sans-serif;
    }
</style>