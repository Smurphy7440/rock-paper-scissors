<template>
    <div class="results">
        <span class="you-picked">You Picked</span><span class="house-picked">The House Picked</span>
        <div class="res your-choice">
            <Paper class="choice" v-if="isPaper" />
            <Scissors class="choice" v-else-if="isScissors" />
            <Rock class="choice" v-else />
        </div>
        <div class="res house-choice">
            <Paper class="comp-choice" v-if="compChosePaper" />
            <Scissors class="comp-choice" v-else-if="compChoseScissors" />
            <Rock class="comp-choice" v-else />
        </div>
        <span class="won-lost">{{resString}}</span>
    </div>
</template>

<script>

import Rock from './Rock';
import Paper from './Paper';
import Scissors from './Scissors';

export default{
    mounted:function(){
        this.removeRes();
    },
    name: 'Results',
    props:['choice', 'machine_choice', 'resString'],
    computed:{
        isPaper: function(){
            return this.choice == "paper";
        },
        isScissors: function(){
            return this.choice == "scissors";
        },
        compChosePaper:function(){
            return this.machine_choice == "paper";
        },
        compChoseScissors:function(){
            return this.machine_choice == "scissors";
        }
    },
    methods:{
        removeRes: function(){
            var myVue = this;
            setTimeout(function(){
                //console.log("Three seconds later...");
                myVue.$emit('changeSelect', false);
            }, 2000);
        }
    },
    components:{
        Rock,
        Paper,
        Scissors
    }
}
</script>

<style>
    .results{
        color: #fffffe;
        height: 100%;
        position: relative;
    }
    span{
        font-size: 35px;
        font-weight: bold;
        text-transform: uppercase;
    }
    .you-picked{
        position: absolute;
        top:10%;
        left: 15%;
    }
    .house-picked{
        position: absolute;
        top:10%;
        left: 55%;
    }

    .won-lost{
        position: absolute;
        left: 40%;
        top: 83%;
    }

    .res{
      /* border: 2px solid #576580; */
      position: absolute;
      height: 40%;
      width:25%;
    }

    .your-choice{
        position: relative;
        left: 12%;
        top: 35%;
    }

    .house-choice{
        position: absolute;
        left:58%;
        top:35%;
    }

    .choice{
        position: absolute;
        left:25%;
        top: 18%;
        transform: scale(2);
    }

    .comp-choice{
        position:absolute;
        left: 25%;
        top: 18%;
        transform: scale(2);
    }


</style>
