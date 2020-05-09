<template>
  <div class="wrapper-popup" v-bind:class="getClassPopup">
    <div class="rule">
        <h1>Luật chơi</h1>
        <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries,</p>
            <button 
            v-on:click="confirm"
            class="Ok">Đã Hiểu
            </button>
    </div>

  </div>
</template>

<script>
export default {
    //
    name:"PopupRule",
    props:{
        isOpenPopup:{type:Boolean, default:false}
    },
    data() {
        return {
            
        }
    },
    computed:{
        getClassPopup:function(){
            return {
                'open-popup':this.isOpenPopup
            }
        }
    },
    methods: {
        confirm(){
            console.log('confirm nằm trong popupRules.vue');
            this.$emit('handleConfirm');
        }
    },
}
</script>

<style>
/* đè lên phía trên */
.wrapper-popup{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.4);
    opacity: 0;
    visibility: hidden;
}
.wrapper-popup.open-popup{
    opacity: 1;
    visibility: visible;
    transition: all .3s ease;
}
.rule{
    padding:  20px;
    position: absolute;
    background: white;
    width: 300px;
    top:50%;
    left: 50%;
    transform: translate(-50%,-50%) scale(1.2);
}
.open-popup .rule{
    transform: translate(-50%,-50%) scale(1);
    transition: all .3s ease;
}
.Ok{
 display: block;
 margin: 10px 100px;
 width: 50px;
 height: 50px;
 border-radius:2px;
 transition: all .5s ease;
}
.Ok:hover{
     background-color: aquamarine;
    color:green;
    cursor: pointer;
   


   
}
</style>