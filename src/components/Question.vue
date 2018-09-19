<template>

        <div class="card">
            <div class="card-header">
                <h3 class="panel-title text-center">{{question}}</h3>
            </div>
            <div class="card-body">
                <div class="row">
                    <div class="col-xs-12 col-sm-6 text-center">
                        <button class="btn btn-primary btn-lg" style="margin: 10px" @click="onAnswer(btnData[0].correct)">{{btnData[0].answer}}</button>
                    </div>
                    <div class="col-xs-12 col-sm-6 text-center">
                        <button class="btn btn-primary btn-lg" style="margin: 10px" @click="onAnswer(btnData[1].correct)">{{btnData[1].answer}}</button>
                    </div>
                    <div class="col-xs-12 col-sm-6 text-center">
                        <button class="btn btn-primary btn-lg" style="margin: 10px" @click="onAnswer(btnData[2].correct)">{{btnData[2].answer}}</button>
                    </div>
                    <div class="col-xs-12 col-sm-6 text-center">
                        <button class="btn btn-primary btn-lg" style="margin: 10px" @click="onAnswer(btnData[3].correct)">{{btnData[3].answer}}</button>
                    </div>
                </div>
            </div>
        </div>

</template>

<script>
    const MODE_ADDITION = 1;
    const MODE_SUBSTRATION = 2;
    export default {
        name: "question",
        data(){return{
            question:'Oops an error occurred:/',
            btnData:[
                {correct:true, answer:0},
                {correct:false, answer:0},
                {correct:false, answer:0},
                {correct:false, answer:0},
            ]
        }},
        methods:{
            generateQuestion(){
                const firstNumber = this.generateRandomNumber(1,100)
                const secondNumber = this.generateRandomNumber(1,100)
                const modeNumber = this.generateRandomNumber(1,2)

                let correctAnswer = 0

                switch (modeNumber)
                {
                    case  MODE_ADDITION:
                        correctAnswer = firstNumber + secondNumber
                        this.question= `What's ${firstNumber} + ${secondNumber}`
                        break;
                    case  MODE_SUBSTRATION:
                        correctAnswer = firstNumber - secondNumber
                        this.question= `What's ${firstNumber} - ${secondNumber}`
                        break;
                    default: correctAnswer = 0
                        question = 'Oops an error occurred:/'
                }
                this.btnData[0].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10,correctAnswer)
                this.btnData[0].correct = false
                this.btnData[1].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10,correctAnswer)
                this.btnData[1].correct = false
                this.btnData[2].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10,correctAnswer)
                this.btnData[2].correct = false
                this.btnData[3].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10,correctAnswer)
                this.btnData[3].correct = false

                let correctButton = this.generateRandomNumber(0,3)
                this.btnData[correctButton].correct = true
                this.btnData[correctButton].answer = correctAnswer

            },
            generateRandomNumber(x,y,except){
                const rndNumber = Math.round(Math.random() * (y - x)) + x
                console.log(x,y,rndNumber)

                if(rndNumber == except)
                {
                    return this. generateRandomNumber(x,y,except)
                }
                return rndNumber
            },
            onAnswer(isCorrect){
                this.$emit('answered',isCorrect)
            }

        },
        created(){
            this.generateQuestion()
        }
    }
</script>

<style scoped>

</style>