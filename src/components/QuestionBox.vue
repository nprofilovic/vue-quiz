<template>
  <div class="jumbotron">
    <p class="lead">{{currentQuestion.question}}</p>
    <hr class="my-4">
      <ul class="list-group">
        <li class="list-group-item" 
          @click.prevent="selectAnswer(index)" 
          :class="answerClass(index)" 
          v-for="(answer, index) in answers" 
          :key="index">
            {{answer}}
        </li>
      </ul>
    <button :disabled="selectedIndex === null || answered" @click="submitAnswer" role="button" class="btn btn-primary btn-lg" >Submit</button>
    <button @click="next" class="btn btn-success btn-lg" role="button">Next</button>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
  name: 'QuestionBox',
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  data () {
    return {
      selectedIndex: null,
      correctIndex: null,
      shuffledAnswers: [],
      answered: false
    }
  },
  
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null
        this.answered = false
        this.shuffleAnswers()
      }
    }
  },
  methods: {
    selectAnswer(index) {
      this.selectedIndex = index
    },
    shuffleAnswers() {
      let answer = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers = _.shuffle(answer)
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    },  
    submitAnswer() {
      let isCorrect = false
      if(this.selectedIndex === this.correctIndex) {
        isCorrect = true
      }
      this.answered = true
      this.increment(isCorrect)
    },
    answerClass(index) {
      let answerClass = ''

      if(!this.answered && this.selectedIndex === index) {
        answerClass = 'selected'
      } else if (this.answered && this.correctIndex === index) {
        answerClass = 'correct'
      } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
        answerClass = 'incorrect'
      }

      return answerClass

    }
  },
  
  
  
}
</script>

<style scoped>
  .list-group {
    margin-bottom: 15px;
  }
  .list-group-item:hover {
    background: #EEE;
    cursor: pointer;
  }
  .btn {
    margin: 0 5px;
  }
  .selected {
    background-color: lightblue
  }
  .correct {
    background-color: lightgreen
  }
  .incorrect {
    background-color: lightcoral
  }
</style>