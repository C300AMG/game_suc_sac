<template>
  <div class="wrapper-controls">
       <button 
       v-on:click="newGame"
       class="control btn-new"><i class="ion-ios-plus-outline"></i>New game</button>
       
        <button 
        v-on:click="rollDice"
        class="control btn-roll"><i class="ion-ios-loop"></i>Roll dice</button>
        <button 
        v-on:click="$emit('HandleHoldScore')"
        class="control btn-hold"><i class="ion-ios-download-outline"></i>Hold</button>
        <input 
        
        v-bind:disabled="isPlaying"
        v-bind:value="finalScore"
        v-on:input="handleInput"
        type="number" placeholder="Final score" class="final-score">
        <!-- <input 
        
        v-bind:value="valueDemo"
        v-on:input="handleInput"
        type="number" placeholder="Final score" class="final-score"> -->
  </div>
</template>

<script>
// bây giờ  finalScore nó nằm ở control, mình muốn dữ liệu đó được lấy ở data App
//Vì sao phải lấy dữ liệu ở App. bởi vì ở thằng App mình mới kích hoạt dc sự kiện
// khi nó đủ điểm thì :
 // +Dừng game lại 
 // +cập nhật điểm ScorePlayer 
 // + Đổi class player thành winer,...


/*
Từ data App 
-> truyền ra : (v-bind)  sau đó mấy cbn CON nhận bằng props
-> Nhận vào  cái sự mong muốn của thằng cbn Con
  --> Đầu tiên thằng con dùng cái event  v-on:click="newGame" để gửi lên data App
  -->Thằng data App muốn nhận được phải tạo 1 cái method có sự kiện (tự tạo)
   v-on:handleNewGame="handleNewGame"
   Sau đó xử lý thay đổi theo ý muốn của thằng con
  --> Thay đổi ok rồi thì thằng con muốn nhận thì trong cái sự kiện ban đầu nó gửi 
  rollDice (){ trong này this.$emit('su kien tu tao ben app')}
***************
Quay lại bài ScoreFInal
--> Đầu tiên trong data App truyền finalScore cho ông control bằng cách 
v-bind:finalScore="finalScore"
--> , ông controls nhận bằng cách 
 props:{
      finalScore:{type:Number, default:100}
    },
--> Ông con ổng nhận rồi giờ ổng muốn thay đổi finalScore đó và muốn bên Data App nhận được và thay đổi theo ý ổng, bây giờ không dùng được ràng buộc 2 chiều v-model
Vì đó là props(đươc nhận từ thằng app) chứ không phải data của chính thằng con nên 
không thể dùng v-model

Thay vào đó ta dùng gán dữ liệu 1 chiều: 
v-bind:value="finalScore" để thay đổi props nó nhận từ app
và dùng 1 cái sự kiện khác,
 khi người dùng có sự thay đổi thì kích hoạt 1 cái sự kiện để làm thay đổi props
 v-on:input="handleInput"
 trong cái method này 
   handleInput(e){
       this.$emit('handleChangeFinalScore',e);
 
      },
      nó truyền cái event(trong này có toàn bộ dl của ô input) bằng this.$emit(handleChangeFinalScore=> tên sự kiện tự tạo để nhận sự thay đổi của thằng con)
--> Cuối cùng bên app cái sự kiện tự tạo handleChangeFinalScore đã nhận dc event của thằng con(cONTROLS.VUE)

-->Tiếp theo gán dl ra gán vào trong datap App.vue là xong Lưu ý sự kiện dcc truyền từ ô input qua nó là dạng chuỗi Bởi vậy mình phải ép kiểu dạng số rồi cho vào data

    ------->


*/
export default {
    name:"Controls",
    props:{
      finalScore:{type:[Number,String], default:100},
      isPlaying:Boolean
    },
 
    data() {
        return {
            valueDemo :100
        }
    },
    methods:{
      handleInput(e){
       this.$emit('handleChangeFinalScore',e);
       
        
      },
     
      newGame(){
        console.log('newGame từ trong Component Controll.vue');
        //kích hoạt cái sự kiện vừa mới tạo ở component App $emit(ten su kien, tham so truyen ra bên ngoai)
        // v-on:handleNewGame="handleNewGame" 
        //ten su kien la thang sau v-on
        // con trong ngoac kep la ten methods 
        this.$emit('handleNewGame');
      },
      rollDice(){
        console.log('rollDice ở trong component Controls.vue');
        this.$emit('handlerollDice');
      }
    },
    components:{

    }

}
</script>

<style>

</style>