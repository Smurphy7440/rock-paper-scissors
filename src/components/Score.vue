<template>
    <div class="score-header">
        <div class="score-words">
            <h4 class="rock">Rock</h4>
            <h4 class="rock">Paper</h4>
            <h4 class="rock">Scissors</h4>
        </div>
        <div class="score" @click="reset">
            <p class="score-p">SCORE</p>
            <h2 class="score-num">{{score}}</h2>
        </div>

    </div>
</template>

<script>

export default{
    name:'Score',
    props:['score'],
    methods:{
        reset: function(){
            this.$emit('reset', 0);
        }
    }
}
</script>

<style>
.score-header{
    color: #fffffe;
    width:50%;
    margin: auto;
    border: 2px solid #576580;
    border-radius: 5px;
    height: 60px;
    padding-top: 5px;
    padding-bottom: 5px;
}
.rock{
    margin: 0px;
    width: 50%;
    padding-left: 5px;
    text-transform: uppercase;
}

.score-words{
    width: 50%;
    margin: 0px 0px;
    float: left;
}

.score{
    width: 25%;
    float:left;
    margin-left: 23%;
    margin-top: 2.5px;
    margin-bottom: 2.5px;
    color: #686771;
    background-color: #fafafa;
    border-radius: 5px;
    text-align: center;
    padding-top: 5px;
    padding-bottom: 5px;
}

.score-p{
    margin: 0px;
}

.score-num{
    margin: 0px;
    cursor: pointer;
}

</style>
