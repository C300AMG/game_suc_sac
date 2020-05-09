<template>

	<div id="app">
	  <div class="wrapper clearfix">
          <players 
          v-bind:isWinner="isWinner"
          v-bind:PlayerScore="PlayerScore"
          v-bind:ScoreCurrent="ScoreCurrent"
          v-bind:Active="Active">
          </players>
            

            <!-- 

                finalScore :
                 v-bind:finalScore="finalScore" đầu tiên là 
                 v-on:handleChangeFinalScore="handleChangeFinalScore"


             -->
           <Controls 

        
           v-bind:finalScore="finalScore"
           v-on:handleChangeFinalScore="handleChangeFinalScore"


            v-bind:isPlaying="isPlaying"
           v-on:HandleHoldScore="HandleHoldScore"
           v-on:handleNewGame="handleNewGame"
           v-on:handlerollDice="handlerollDice">
           
           </Controls>
         
            <Dices v-bind:dices="dices"></Dices>
 
            <PopupRule
            v-on:handleConfirm="handleConfirm"
            v-bind:isOpenPopup="isOpenPopup">
            </PopupRule>
           
        </div>
	</div>
</template>

<script>
import PopupRule from './components/PopupShowRule.vue';
import Players from './components/Players.vue';
import Controls from './components/Controls.vue';
import Dices from './components/Dices.vue';
export default {
	name: 'app',
	data () {
		return {
            isOpenPopup:false,
            isPlaying:false,
            PlayerScore:[0,0],
            ScoreCurrent:30,
            Active:0,
            dices:[5,2],
            finalScore:10
           
		}
    },
    computed: {
        // khai báo những hàm tự động được chạy bất kể khi nào dl bên trong có sự thay đổi 
        isWinner(){
            let{PlayerScore,finalScore} = this
            /*
            so sánh nêu như PlayerScore >= finalScore của người chơi thứu 1 hoặc PlayerScore >= finalScore của người chơi thứ 2 thì tiến hành:
                Dừng cuộc chơi và returrn về true để người chơi dùng cái biến isWinner này để gắn vào class player

             */
            if(PlayerScore[0] >= finalScore || PlayerScore[1] >= finalScore){
                this.isPlaying = false; //Dừng cuộc chơi
                return true;
            }else{
                  return false; // nếu không có ai chiến thằng thị isWinner không làm j
            }
          
            
        }
    },
    methods: {
        handleChangeFinalScore(e){
            var number = parseInt(e.target.value);
                if(isNaN(number)){
                // chuỗi rỗng
                  this.finalScore = " ";
            }else{
                this.finalScore = number;
            };
              console.log(e.target.value,'Đây là dữ liệu event đươcu truyền qua từ controls');
        
        },
        HandleHoldScore(){
            if(this.isPlaying){
            let {PlayerScore ,Active, ScoreCurrent} = this;
            let scoreOld = PlayerScore[Active];
            let ClonePlayerScore = [...PlayerScore];
                ClonePlayerScore [Active] = scoreOld + ScoreCurrent;
                 this.PlayerScore = ClonePlayerScore;
                console.log(ClonePlayerScore [Active]);
               if(!this.isWinner){
                    this.nextPlayer();
               }
            }else{
                alert('Vui lòng nhấn vào nút new game để thực hiện chức năng này !!!');
            }
            
        },
         nextPlayer(){
                //activePlayer = 0 --- đổi lại = 1 và ngược lại
                //cho 1 cai bien = thang nay co = 0 hay khong , neu nhu dieu kiẹn nay dung thi no tra = 1
                // va : nguoc lai neu nhu dieu kien nay sai thi no bang 0
                this.Active = this.Active === 0 ? 1 : 0;
                this.ScoreCurrent =0;
         },
        handlerollDice(){
           
            console.log('handlerollDice trong component app.vue');
            if(this.isPlaying){
                // xoay xúc sắc
                var dice1 =Math.ceil( Math.random()*6);
                var dice2 =Math.ceil( Math.random()*6);
                console.log(dice1,dice2);
                this.dices = [dice1,dice2];
                // kiểm tra nếu 1 trong 2 dice = 1 thì tiến hành đổi lượt chơi và reset điểm tạm thời = 0
                // nếu không quay vào 1 thì + zồn vào thôi



                if(dice1===1 || dice2 ===1){
                    // đổi lợt chơi
                     let Active = this.Active;
                    setTimeout(function(){
                            alert(`RẤT TIẾC NGƯỜI CHƠI ${Active +1} đã mất lượt chơi`);
                    }, 10)
                    this.nextPlayer();
                    //reset điểm lại
                }else{
                    // cộng dôn vào curentSCORE 
                     this.ScoreCurrent = this.ScoreCurrent +dice1+dice2
                }
            }else{
                alert('Vui lòng nhấn vào nút new Game');
            }
            
        },
        handleNewGame(){
        console.log('handleNewGame từ trong component App.vue');
        this.isOpenPopup = true;
        },
           
        handleConfirm(){
            console.log('handleConfirm trong App.vue');
            this.isPlaying = true;
            this.isOpenPopup = false,
            this.Active = 0;
            this.dices = [1,1];
            this.PlayerScore = [0, 0],
            this.ScoreCurrent = 0;
        },
     
    },
	components: {
    Players,
    Controls,
    Dices,
    PopupRule
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
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/public/assets/back.jpg');
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
