<template>
    <div class="wrapper-message2" v-bind:class="getClassEnterFinalScore">
        <div class="message2">
            <h3>Note!</h3>
            <p>You have not entered points. Please enter your score to start the game</p>
            <button v-on:click="closeNote" class="button">Close</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'message-2',
    data(){
        return{

        }
    },
    props:{
        isEnterFinalScore: {
            type: Boolean,
            default: false
        }
    },
    computed:{
        getClassEnterFinalScore(){
            return{
                'open-message2': this.isEnterFinalScore
            }
        }
    },
    methods:{
        closeNote(){
            //console.log('closeNote from Message2.vue')
            this.$emit('handleCloseNote')
        }
    }
}
</script>

<style>
.wrapper-message2{
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
.wrapper-message2.open-message2{
        opacity: 1;
        visibility: visible;
    }
.message2{
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
.open-message2 .message2{
        transform: translate(-50%, -50%) scale(1);
    }
.message2 h3{
        margin-bottom: 10px;
        color: yellow;
    } 
.message2 .button{
        border:2px solid #333;
        background-color: white;
        padding: 8px 15px;
        transition: all .3s ease;
        margin-top: 10px;
        float: right;
    }
.message2 .button:hover{
        cursor: pointer;
        background-color: #333;
        color:#fff;
    }  
</style>