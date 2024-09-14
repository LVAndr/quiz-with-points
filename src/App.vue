<script setup>
const heroTitle = 'Take the quiz, get a discount!'
</script>

<template>
  <div class="quiz">
    <h1 class="title">{{heroTitle}}</h1>
    <div class="quizBox">
      <div>
        <h2 class="question">Lorem ipsum dolor sit amet, consectetur hola?</h2>
        <ul class="answerOptions">
          <li class="answerOption">Lorem ipsum dolor sit.</li>
          <li class="answerOption active">Lorem ipsum dolor sit.</li>
          <li class="answerOption">Lorem ipsum dolor sit.</li>
          <li class="answerOption">Lorem ipsum dolor sit.</li>
          <li class="answerOption">Lorem ipsum dolor sit lol.</li>
          <li class="answerOption">Lorem ipsum dolor sit lol.</li>
          <li class="answerOption">Lorem ipsum dolor sit lol.</li>
        </ul>
      </div>
      <div class="buttons">
        <button class="btn" disabled>Previous</button>
        <button class="btn">Submit</button>
        <button class="btn">Next</button>
      </div>
    </div>
  </div>

</template>

<style scoped>
h1{
  font-size: 34px;
  margin-top: 30px;
  margin-bottom: 30px;
}
.title{
  text-align: center;
}
h2{
  font-size: 28px;
  color: #210404;
}
.quizBox{
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  padding: 30px 25px;
  margin: 0 auto;
  max-width: 600px;
  min-height: 200px;
  border-radius: 12px;
  background-color: #fff;
}
.answerOptions{
  margin: 25px auto;
}
.answerOption{
  color: #210404;
  font-weight: 500;
  font-size: 20px;
  cursor: pointer;
}
.answerOption:not(:last-child){
  margin-bottom: 12px;
}
.answerOption.active{
  color: #ED2224;
}
.buttons{
  display: flex;
  justify-content: space-between;
  gap: 10px;
  padding: 10px 5px 0;
}
.btn{
  font-weight: 400;
  min-width: 100px;
  padding: 8px 14px;
  border: 1px solid #210404;
  border-radius: 18px;
  transition: all .2s;
}
.btn:disabled{
  border: 1px solid #b2b2b2;
  color: #b2b2b2;
}
.btn:disabled:hover{
  background-color: transparent;
}
.btn:disabled:active{
  color: #b2b2b2;
}
.btn:hover{
  background-color: #b9c0cb;
}
.btn:active{
  color: #ED2224;
}
</style>
