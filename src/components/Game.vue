<template>
    <div class="game-window">
        <div v-if="!computedSelected" class="choice-window">
            <Paper @click="Click" class="paper-comp"/>
            <Scissors @click="Click" class="scissors-comp" />
            <Rock @click="Click" class="rock-comp"/>
        </div>
        <div v-else class="result-window">
            <Results @changeSelect="removeIt" :resString="resString" :choice="choice" :machine_choice="machine_choice" />
        </div>
    </div>

</template>

<script>
import Paper from './Paper';
import Scissors from './Scissors';
import Rock from './Rock';
import Results from './Results';


export default{
    name: 'Game',
    data: function(){
        return{
            options: ['rock', 'paper', 'scissors'],
            selected: false,
            won: false,
            choice: '',
            machine_choice:''
        }
    },
    components:{
        Paper,
        Scissors,
        Rock,
        Results
    },
    methods:{
        Click(e){
            this.selected = !this.selected;
            if(e.target.className == "paper paper-comp"){
                this.choice = "paper";
            }else if(e.target.className == "scissors scissors-comp"){
                this.choice = "scissors";
            }else{
                this.choice = "rock";
            }
            this.machine_choice = this.options[Math.floor(Math.random()*this.options.length)];
            // console.log('You clicked ' + e.target.className);
            // console.log(this.machine_choice);

            this.wonOrLost();
        },
        wonOrLost(event){
            switch(this.machine_choice){
                case 'rock':
                    this.won = this.choice == 'paper' ? true: (this.choice == 'rock' ? 'draw' : false);
                    break;
                case 'paper':
                    this.won = this.choice == 'scissors' ? true: (this.choice == 'paper' ? 'draw' : false);
                    break;
                case 'scissors':
                    this.won = this.choice == 'rock' ? true: (this.choice == 'scissors' ? 'draw' : false);
                    break;
            }

            this.$emit('wonOrLost', this.won);
        },
        removeIt(value){
            this.selected = value;
        }
    },
    computed:{
        resString: function(){
            if(this.won == true){
                return "YOU WON";
            }else if(this.won == false){
                return "YOU LOST";
            }else{
                return "DRAW";
            }
        },
        computedSelected: function(){
            return this.selected;
        }
    }
}
</script>

<style>
    .choice-window{
        width: 100%;
        margin: auto;
        /* border: 2px solid #576580; */
        height: 100%;
        background-image: url(../assets/bg-triangle.svg);
        background-repeat: no-repeat;
        background-attachment:inherit;
        background-position: 50% 65%;
        background-size: 400px 300px;
        position: relative;
    }

    .result-window{
        width: 100%;
        margin: auto;
        height: 100%;
        /* border: 2px solid #576580; */
    }

    .game-window{
        width: 75%;
        margin: auto;
        height: 70%;
    }

    .paper-comp{
        float: left;
        position: absolute;
        left: 25%;
        transition: transform .2s;
        top: 15%;
    }

    .paper-comp:hover{
        transform: scale(1.2);
    }

    .scissors-comp{
        float:left;
        position: absolute;
        transition: transform .2s;
        left: 62%;
        top: 15%;
    }

    .scissors-comp:hover{
        transform: scale(1.2);
    }

    .rock-comp{
        float: left;
        position: absolute;
        transition: transform .2s;
        left: 44%;
        top: 70%;
    }

    .rock-comp:hover{
        transform: scale(1.2);
    }

</style>
