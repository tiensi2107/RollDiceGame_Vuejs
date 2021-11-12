<template>
    <div class="wrapper-message" v-bind:class="getClassMessage">
        <div class="message">
            <h3>Warning!</h3>
            <p>
                Please enter <strong>NEW GAME</strong> button to start game.
            </p>
            <button v-on:click="close" class="button">Close</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'message',
    data(){
        return{

        }
    },
    props:{
        isOpenMessage: {
            type: Boolean,
            default: false
        }
    },
    computed:{
        getClassMessage(){
            return{
                'open-message': this.isOpenMessage
            }
        }
    },
    methods:{
        close(){
            //console.log('close from Message.vue')
            this.$emit('handleClose')
        }
    }
}
</script>

<style>
.wrapper-message{
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
.wrapper-message.open-message{
        opacity: 1;
        visibility: visible;
    }
.message{
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
.open-message .message{
        transform: translate(-50%, -50%) scale(1);
    }
.message h3{
        margin-bottom: 10px;
        color: red;
    } 
.message .button{
        border:2px solid #333;
        background-color: white;
        padding: 8px 15px;
        transition: all .3s ease;
        margin-top: 10px;
        float: right;
    }
.message .button:hover{
        cursor: pointer;
        background-color: #333;
        color:#fff;
    }  
</style>