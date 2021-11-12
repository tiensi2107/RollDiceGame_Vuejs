<template>
    <div class="wrapper-message3" v-bind:class="getDiceValue1">
        <div class="message3">
            <h3>Sorry!</h3>
            <p>You rolled the dice of value 1. So you lost your turn</p>
            <button v-on:click="closeDiceValue1" class="button">Close</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'message-3',
    data(){
        return{

        }
    },
    props:{
        isDiceValueOne: {
            type: Boolean,
            default: false
        }
    },
    computed:{
        getDiceValue1(){
            return{
                'open-message3': this.isDiceValueOne
            }
        }
    },
    methods:{
        closeDiceValue1(){
            this.$emit('handleCloseDiceValue1')
        }
    }
}
</script>

<style>
.wrapper-message3{
    position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0, 0, 0, 0.4);
        opacity: 0;
        visibility: hidden;
        transition: all .3s ease;
}
.wrapper-message3.open-message3{
        opacity: 1;
        visibility: visible;
    }
.message3{
        position: absolute;
        background-color: #fff;
        width: 350px;
        padding: 20px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) scale(1.2);
        font-family: Arial, Helvetica, sans-serif;
        transition: all .3s ease;
    }
.open-message3 .message3{
        transform: translate(-50%, -50%) scale(1);
    }
.message3 h3{
        margin-bottom: 10px;
        color: Blue;
    } 
.message3 .button{
        border:2px solid #333;
        background-color: white;
        padding: 8px 15px;
        transition: all .3s ease;
        margin-top: 10px;
        float: right;
    }
.message3 .button:hover{
        cursor: pointer;
        background-color: #333;
        color:#fff;
    }  
</style>