<template>
  <div class="jumbotron">
    <p class="lead">{{currentQuestion.question}}</p>
    <hr class="my-4">

      <ul class="list-group">
        <li class="list-group-item" v-for="(answer, index) in answers" :key="index">{{answer}}</li>
      </ul>
      
    <a class="btn btn-primary btn-lg" href="#" role="button">Submit</a>
    <a @click="next" class="btn btn-success btn-lg" href="#" role="button">Next</a>
  </div>
</template>

<script>
export default {
  name: 'QuestionBox',
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  props: {
    currentQuestion: Object,
    next: Function
  },
  
}
</script>

<style>

</style>