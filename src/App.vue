<template>
  <div id="app">
    <Header :numCorrect="numCorrect" :numTotal="numTotal" />
    <div class="row">
      <div class="col-sm">
       
      </div>
      <div class="col-sm">
        <QuestionBox v-if="questions.length" :currentQuestion ="questions[index]" :next= "next" :increment = "increment"/>
      </div>
      <div class="col-sm">
        
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods:{
    next() {
      this.index++
    },
    increment(isCorrect) {
      if(isCorrect) {
        this.numCorrect++
      }
      this.numTotal++
    }
    
  },
  mounted: function() {
      axios.get('https://opentdb.com/api.php?amount=10&category=11&type=multiple')
      .then(response => this.questions = response.data.results)
      .catch(err => console.log(err))
      
    }
  }

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
