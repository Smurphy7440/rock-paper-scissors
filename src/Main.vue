<template>
  <div class="main-screen">
    <Score @reset="reset" :score="yourScore" />
    <Game @wonOrLost="getWin" />
    <Modal class="the-modal" v-show="isModalVisible" @close="closeModal" />
    <button @click="showModal" class="rules">Rules</button>
  </div>
</template>

<script>

import Score from './components/Score';
import Game from './components/Game';
import Modal from './components/Modal';

export default {
  mounted(){
    //localStorage.setItem("score", 0);
    //this.score = 0;
  },
  name: 'Main',
  data: function(){
    return {
      score: Number(localStorage.getItem("score")),
      val: '',
      isModalVisible: false
    }
  },
  components: {
    Score,
    Game,
    Modal
  },
  methods:{
    getWin: function(value){
      //console.log(value);
      switch(value){
        case true:
          this.score += 2;
          this.val = 'WON';
          break;
        case false:
          this.score -= 1;
          this.val = 'LOST';
          break;
        case 'draw':
          this.val = 'DRAW'
      }
    },
    reset: function(value){
      //console.log("This is Main, I got an emit from Score. Value: " + value);
      localStorage.setItem("score", value);
      this.score = Number(localStorage.getItem("score"));
    },
    showModal: function(){
      this.isModalVisible = true;
    },
    closeModal: function(){
      this.isModalVisible = false;
    }
  },
  computed:{
    yourScore: function(){
      if(this.score <= 0){
        localStorage.setItem("score", 0)
        this.score = 0;
        return 0;
      }else{
        localStorage.setItem("score", this.score)
        return this.score;
      }
    }
  }
}
</script>

<style>
.main-screen{
  height: 100%;
  background: radial-gradient(#1e3253, #182343) ;
  padding-top: 25px;
  padding-right: 25px;
  padding-left: 25px;
  position: relative;
}

  .rules{
      color: #c0c5ce;
      font-size: 16px;
      padding: 15px 15px;
      width: 150px;
      border: 2px solid #576580;
      transition: transform .2s;
      border-radius: 10px;
      font-weight: bold;
      background-color: #15193c;
      text-transform: uppercase;
      position: absolute;
      left: 85%;
      top: 85%;
  }

  .rules:hover{
    transform: scale(1.1);
  }

  .the-modal{
    position: relative;
    bottom: 55%;
    left: 25%;
    height: 100%;

  }

</style>
