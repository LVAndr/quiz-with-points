<script setup>
const heroTitle = 'Take the quiz, get a discount!'
</script>

<template>
  <div class="quiz">
    <h1 class="title">{{heroTitle}}</h1>
    <div class="quizBox">
      <h2 class="answer">Lorem ipsum dolor sit amet, consectetur.?</h2>
      <ul class="answerOptions">
        <li class="answerOption">Lorem ipsum dolor sit.</li>
        <li class="answerOption">Lorem ipsum dolor sit.</li>
        <li class="answerOption">Lorem ipsum dolor sit.</li>
      </ul>
      <div class="buttons">
        <button class="btn">Previous</button>
        <button class="btn">Submit</button>
        <button class="btn">Next</button>
      </div>
    </div>
  </div>

</template>

<style scoped>
h1{
  margin-top: 30px;
  margin-bottom: 30px;
}
.title{
  text-align: center;
}
.quizBox{
  padding: 30px 25px;
  margin: 0 auto;
  max-width: 600px;
  min-height: 200px;
  border-radius: 12px;
  background-color: #fff;
}
.btn{
  background-color: #ED2224;
}
</style>
