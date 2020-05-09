<template>
  <div class="wrapper-player">
              <!-- player 1 -->
            <div class="player-panel " v-bind:class="{
                active: Active == 0 && !this.isWinner,
                winner :Active ==0 && this.isWinner

            
            }">
                <div class="player-name">{{getNamePlayer(0)}}</div>
                <div class="player-score">{{ PlayerScore[0] }}</div>
                <div class="player-current-box">
                    <div class="player-current-label">Current</div>
 <!--  neu active = 0 tuc la thang dau tien choi truoc, no la nguoi choi thi gan cho no bang ScoreCurrent, tuc la diem current cua no phai co,nguoc lai neu khong phai thi ScoreCurrent lay gia tri = 0 boi vi no khong co luot choi -->
                    <div class="player-current-score">{{ Active == 0 ? ScoreCurrent : 0}}</div>
                </div>
            </div>
            <!-- player 2 -->
            <div class="player-panel" v-bind:class="{
                active: Active == 1 && !this.isWinner,
                winner :Active ==1 && this.isWinner
                }">
                <div class="player-name">{{getNamePlayer(1)}}</div>
                <div class="player-score">{{ PlayerScore[1] }}</div>
                <div class="player-current-box">
                    <div class="player-current-label">Current</div>

                    <div class="player-current-score">{{ Active == 1 ? ScoreCurrent : 0}}</div>
                </div>
            </div>
  </div>
</template>

<script>
export default {
    name:"players",
    props:{
        PlayerScore:{
            PlayerScore:Array,
            default:[0,0]
        },  
        ScoreCurrent:{
            PlayerScore:Number,
            default:0
        },
          Active:{
            PlayerScore:Number,
            default:0
        },
        isWinner:{type:Boolean, default:false}
    },
    data() {
        return {
            
        }
    },
    methods: {
            getNamePlayer(index){
                var  defaultName = 'Player' +(index +1); 
                console.log(index, defaultName, this.isWinner, this.Active);
                if(this.Active == index && this.isWinner){
                    defaultName = 'Winner !!!';
                } return defaultName;
            }
    },
}
</script>

<style>
/**********************************************
*** PLAYERS
**********************************************/
.player-panel {
    width: 50%;
    float: left;
    height: 600px;
    padding: 100px;
    transition: all .3s ease;
    background-color: #fff;
}
.player-name {
    font-size: 40px;
    text-align: center;
    text-transform: uppercase;
    letter-spacing: 2px;
    font-weight: 100;
    margin-top: 20px;
    margin-bottom: 10px;
    position: relative;
}

.player-score {
    text-align: center;
    font-size: 80px;
    font-weight: 100;
    color: #42b983;
    margin-bottom: 130px;
}

.active { background-color: #f7f7f7; }
.active .player-name { font-weight: 300; }

.active .player-name::after {
    content: "\2022";
    font-size: 47px;
    position: absolute;
    color: #42b983;
    top: -7px;
    right: 10px;
    
}

.player-current-box {
    background-color: #42b983;
    color: #fff;
    width: 40%;
    margin: 0 auto;
    padding: 12px;
    text-align: center;
}

.player-current-label {
    text-transform: uppercase;
    margin-bottom: 10px;
    font-size: 12px;
    color: #222;
}

.player-current-score {
    font-size: 30px;
}

.winner { background-color: #f7f7f7; }
.winner .player-name { font-weight: 300; color: #42b983; }
/**********************************************
*** Control
**********************************************/
.control {
    position: absolute;
    width: 200px;
    left: 50%;
    transform: translateX(-50%);
    color: #555;
    background: none;
    border: none;
    font-family: Lato;
    font-size: 20px;
    text-transform: uppercase;
    cursor: pointer;
    font-weight: 300;
    transition: background-color 0.3s, color 0.3s;
}
.control.disable {
    pointer-events: none;
}

.control:hover { font-weight: 600; }
.control:hover i { margin-right: 20px; }

.control:focus {
    outline: none;
}

.control i {
    color: #42b983;
    display: inline-block;
    margin-right: 15px;
    font-size: 32px;
    line-height: 1;
    vertical-align: text-top;
    margin-top: -4px;
    transition: margin 0.3s;
}

.btn-new { top: 45px;}
.btn-roll { top: 403px;}
.btn-hold { top: 467px;}

.final-score {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 520px;
    color: #555;
    font-size: 18px;
    font-family: 'Lato';
    text-align: center;
    padding: 10px;
    width: 160px;
    text-transform: uppercase;
}

.final-score:focus { outline: none; }


</style>