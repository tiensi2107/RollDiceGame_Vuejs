<template>
  <div class="wrapper-popup" v-bind:class="getClasspopup">
        <div class="rule">
            <h3>Rules</h3>
            <ul>
                <li>Click <strong>ROLL DICE</strong> to roll dices. </li>
                <li> If one of the dice is one, the player loses his turn and all current points are lost.</li>
                <li>Click <strong>HOLD</strong> to update score.</li>
                <li>the winner is the one whose score is equal to the set point.</li>
            </ul>
            <button class="button" v-on:click="button">Close</button>
        </div>
  </div>
</template>

<script>
export default {
    name: 'popup',
    data(){
        return{

        }
    },
    props:{
        isOpenPopup:{
            type: Boolean,
            default: false
        }
    },
    methods:{
        button(){
            //truyen event ra parents
            //console.log('button from Popup.vue')
            this.$emit('handleButton')
        }
    },
    computed:{
        getClasspopup(){
            return{
                'open-popup': this.isOpenPopup
            }
        }
    }
};
</script>
    
<style>
    .wrapper-popup{
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
    .wrapper-popup.open-popup{
        opacity: 1;
        visibility: visible;
    }
    .rule{
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
    .open-popup .rule{
        transform: translate(-50%, -50%) scale(1);
    }
    .rule h3{
        margin-bottom: 10px;
        color: green;
    }
    .rule .button{
        border:2px solid #333;
        background-color: white;
        padding: 8px 15px;
        transition: all .3s ease;
        margin-top: 10px;
        float: right;
    }
    .rule .button:hover{
        cursor: pointer;
        background-color: #333;
        color:#fff;
    }
    ul{
        list-style-type: none;
    }
    /*Ket hop CSS3 voi VueJS de xay dung hieu ung Zoom in - Zoom out */
</style>