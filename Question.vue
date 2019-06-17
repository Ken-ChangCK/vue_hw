<template>
    <div class="question-box">
    <b-jumbotron>
      <template slot="lead">
        <h5 v-html="currentQuestion.question"></h5>
        <!-- {{currentQuestion.question}} -->
       <!-- <h5 v-html="currentQuestion.correct_answer"></h5> -->
       <!-- <h5 v-html="index"></h5> -->

      </template>
  <hr>
      <b-list-group >
         <b-list-group-item
           v-for="(answer,index) in shuffledAnswers" 
          :key="index"
          @click="Answerchoose(index)"
          :class="highlightAnswer(index)">
           <!-- //{{answer}} -->
          <div v-html="answer"></div>
        </b-list-group-item>
      </b-list-group>

      <br>
    <b-button variant="primary"
      @click="submitAnswer"
      :disabled="selectedIndex===null || answered " >
        Submit</b-button> 
      <b-button @click="next" variant="success"
      :disabled="!answered || countAns>9||coorect>9">
        Next
      </b-button>
       <br><br>
       <b><b-h3>{{Message}}</b-h3></b>
    </b-jumbotron>
    </div>
</template>
<script>

import _ from 'lodash'

export default {
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  data(){
    return {
      selectedIndex: null,
      shuffledAnswers: [],
      correctIndex: null,
      answered: false,
      yMessage: '',
      countAns: 0,
      coorect:0
    }
  },
  watch: {
    currentQuestion : {
      immediate: true,
      handler(){

        this.selectedIndex = null,
        this.shuffleAnswers()
        this.answered = false,
        this.Message = ''
      }
    }
  },
  methods:{
    Answerchoose(index) {
      if(!this.answered){
        this.selectedIndex = index
      }
      // console.log(index)
    },
    highlightAnswer(index) {
        let retClass = ''

        if(!this.answered && index === this.selectedIndex){
            retClass = 'selected'
        }else if(this.answered && index === this.correctIndex){
          retClass = 'correct'
        }else if(this.answered && index === this.selectedIndex && index !== this.correctIndex){
          retClass ='incorrect'
        }
        return retClass
    },
    submitAnswer(){
      let isCorrect = false

      this.Message = "答錯了.....87";
      this.answered = true

      if(this.selectedIndex === this.correctIndex){
        isCorrect = true
        this.Message = "答對了";
        this.coorect++;
        //  this.Message = this.displayMessage+"\n答對\n"+coorect+"\n題\n";
      }
      this.countAns++;

      if(this.countAns>9){
          this.Message = this.Message+"\r\n"+"****答題結束****";
      }

      this.increment(isCorrect)

    },
    shuffleAnswers(){
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers = _.shuffle(answers)
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    }
  },
  computed: {    
    Answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers;
    }
  }
}
</script>

<style scoped>
.btn {
  margin: 0 10px;
}
.list-group-item:hover {
  background: rgb(207, 18, 18);
  cursor: pointer;
}
.selected {
  background-color: rgb(125, 192, 255);
}
.correct{
  background-color: rgb(153, 255, 153);
}
.incorrect{
  background-color: rgb(255, 160, 160);
}
</style>
