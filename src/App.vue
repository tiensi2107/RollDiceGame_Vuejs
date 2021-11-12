<template>
	<div id="app">
		<div class="wrapper clearfix">
            <players 
                v-bind:isWinner="isWinner"
                v-bind:scorePlayer="scorePlayer"
                v-bind:activePlayer="activePlayer"
                v-bind:currentScore="currentScore"
            />

            <controls 
                v-bind:isPlaying="isPlaying"
                v-on:handleChangeFinalScore="handleChangeFinalScore"
                v-bind:finalScore="finalScore"
                v-on:handleNewGame="handleNewGame"
                v-on:handleRollDices="handleRollDices"
                v-on:handleHoldScore="handleHoldScore"
            />
            
            <dices 
                v-bind:dices="dices"
            />
            
            <popup 
                v-on:handleButton="handleButton"
                v-bind:isOpenPopup="isOpenPopup"
            />

            <message 
                v-bind:isOpenMessage="isOpenMessage"
                v-on:handleClose="handleClose"
            />

            <message-2 
                v-bind:isEnterFinalScore="isEnterFinalScore"
                v-on:handleCloseNote="handleCloseNote"
            />

            <message-3 
                v-bind:isDiceValueOne="isDiceValueOne"
                v-on:handleCloseDiceValue1="handleCloseDiceValue1"
            />
        </div>
	</div>
</template>

<script>
import Players from './components/Players.vue';
import Controls from './components/Controls.vue';
import Dices from './components/Dices.vue';
import Popup from './components/Popup.vue'
import Message from './components/Message.vue';
import Message2 from './components/Messsage2.vue';
import Message3 from './components/Message3.vue';
export default {
	name: 'app',
	data () {
		return {
            scorePlayer: [10, 20],
            currentScore: 30,
            activePlayer: 0, //ai la nguoi choi hien tai
            isPlaying: false, //ng choi co dang choi game hay khong
            isOpenPopup: false,
            dices: [1, 5],
            finalScore: 0,
            isOpenMessage: false,
            isEnterFinalScore: false,
            isDiceValueOne: false
		}
	},
    components: {
        Players,
        Controls,
        Dices,
        Popup,
        Message,
        Message2,
        Message3
    },
    methods:{
        handleChangeFinalScore(e){
            var number = parseInt(e.target.value)
            if (isNaN(number)) {
                this.finalScore = ''
            }else{
                this.finalScore = number
            }
        },
        handleNewGame(){
            //console.log('handleNewGame from App.vue')
            //hien thi Pop-up hien thi luat choi
            if (this.finalScore == 0) {
                this.isEnterFinalScore = true
            }else{
                this.isOpenPopup = true
            }
        },
        handleButton(){
            //console.log('HandleButton from App.vue')
            this.isPlaying = true
            this.isOpenPopup = false
            this.activePlayer = 0
            this.scorePlayer = [0, 0]
            this.currentScore = 0
            this.dices = [1, 1]
        },
        nextPlayer(){
            this.activePlayer = this.activePlayer === 0 ? 1 : 0
            this.currentScore = 0
        },
        handleRollDices(){
            //console.log('handleRollDices from App.vue')
            if(this.isPlaying){
                //tien han xoay xuc xac
                var dice1 = Math.floor(Math.random() * 6) + 1
                var dice2 = Math.floor(Math.random() * 6) + 1

                this.dices = [dice1, dice2]
                //console.log(dice1, dice2)
                if(dice1 === 1 || dice2 === 1){
                    this.isDiceValueOne = true
                    this.nextPlayer()
                }else{
                    //cong don vao diem tam thoi
                    this.currentScore = this.currentScore + dice1 + dice2
                }
            }
            else{
                this.isOpenMessage = true
            }
        },
        handleHoldScore(){
            //console.log('handleHoldScore from App.vue')
            if(this.isPlaying){
                /*let cloneScorePlayer = [...this.scorePlayer];
                let scoreOld = this.scorePlayer[this.activePlayer];
                cloneScorePlayer[this.activePlayer] = scoreOld + this.currentScore;
                this.scorePlayer = cloneScorePlayer;*/
                //console.log(cloneScorePlayer);
                this.$set(this.scorePlayer, this.activePlayer, this.scorePlayer[this.activePlayer] + this.currentScore)
                
                if (!this.isWinner) {
                    this.nextPlayer()
                }
            }else{
                this.isOpenMessage = true
            }
        },
        handleClose(){
            //console.log('handleClose from App.vue')
            this.isOpenMessage = false
        },
        handleCloseNote(){
            //console.log('handleCloseNote from App.vue')
            this.isEnterFinalScore = false
        },
        handleCloseDiceValue1(){
            this.isDiceValueOne = false
        }
    },
    computed:{
        isWinner(){
            if (this.scorePlayer[0] >= this.finalScore || this.scorePlayer[1] >= this.finalScore) {
                //Dung cuoc choi
                this.isPlaying = false
                return true
            }
            return false
        }
    }
	
}
</script>

<style>
	* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url(/public/assets/back.jpg);
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
</style>
