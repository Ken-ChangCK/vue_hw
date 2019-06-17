<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <HelloWorld 
    :numCorrect="numCorrect"
    :numTotal= "numTotal"
    />
    <br><br>
    <!-- <b-button @click="componentKey++">Some</b-button> -->

   <div class="container">  
      <div class="row">
        <!-- <b-col sm="13"></b-col> -->
          <div class="col-sm-12">
          <Question       
            v-if="questions.length" 
            :currentQuestion="questions[index]" 
            :next="next" 
            :increment="increment" /> 
        </div>
        <!-- <b-col sm="5"></b-col> -->
      </div>
    </div>
  </div>
    
</template>

<script>

import HelloWorld from './components/HelloWorld.vue'
import Question from './components/Question.vue'

export default {
  name: 'app',

  components: {
    HelloWorld,
    Question
  },
  data(){
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods: {
    next() {
      this.index++
    },
    increment(isCorrect){

      if(isCorrect){
        this.numCorrect++
        console.log("Correct")
      }
      this.numTotal++
    } 
  },
  mounted: function(){   //=onload()
    fetch("https://opentdb.com/api.php?amount=20&category=21&difficulty=medium&type=multiple",{
      method: 'get'
    })
    .then((res) => res.json())
    .then((data) => {
        this.questions = data.results
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
