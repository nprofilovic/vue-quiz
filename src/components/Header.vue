<template>
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand disabled" href="#"><b>Quiz App</b></a>
    <a class="nav-link disabled" >Counter: {{ numCorrect }} / {{numTotal}} </a>
  </nav>
</template>

<script>
export default {
  name: 'Header',
  props: [
    'numCorrect',
    'numTotal'
  ]
}
</script>

<style>

</style>