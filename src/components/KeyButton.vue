<template>
    <div :class="{Hoverable:!this.disabled,KeyButton:true,disabled:this.disabled,correct:(this.disabled && this.correct),disabled:this.disabled,incorrect:(this.disabled && !this.correct)}" @click.self="Clicked()">
        {{this.ButtonDisplay}}
    </div>
</template>

<script>
export default {
    props:["ButtonDisplay","ID"],
    data:function(){
        return {
            disabled:false,
            // warning:false,
            correct:false
        }
    },
    methods:{
        Clicked:function(){
            if (this.disabled)
                return;
            this.$emit("clicked",this.ButtonDisplay,this.ID,false);
            this.disabled = true;
        },
        Echo:function(){
            alert(this.ID)
        },
        helloWorld:function(){
            alert("Hello World")
        }
    }
}
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
    .KeyButton{
        display: flex;
        background-color: #565656;
        width: 70px;
        height: 70px;
        color: white;
        text-align: center;
        justify-content: center;
        align-items: center;
        border-radius: 20px;
        font-size: 1.5rem;
        box-shadow: 0px 0px 5px 5px green;
        font-family: 'Roboto', sans-serif;
        transition: 0.5s;
    }

    .Hoverable:hover{
        box-shadow: 0px 0px 5px 5px cyan;
        scale: 1.1;
        background: #898989;
    }

    .disabled{
        box-shadow: 0px 0px 5px 5px #676767;
        scale: 0.8;
        background: #676767;
    }

    .incorrect{
        background-color: firebrick;
        box-shadow: 0px 0px 5px 5px rgb(153, 30, 30);
    }

    .correct{
        background-color: purple;
        box-shadow: 0px 0px 5px 5px darkorchid;
    }
</style>