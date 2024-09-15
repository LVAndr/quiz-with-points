<script setup>
import {ref} from "vue";

const heroTitle = 'Take the quiz, get a discount!';
const quizData = ref([
  {
    question: '1Dorem orem ipsum dolor sit amet, consectetur hola?',
    answers: [
      {
        answer: 'Lorem ipsum dolor sit. 1',
        point: 100
      },
      {
        answer: 'Lorem ipsum dolor sit. 1.2',
        point: 200
      },
      {
        answer: 'Lorem ipsum dolor sit. 1.3',
        point: 250
      },
    ]
  },
  {
    question: '2Dorem orem ipsum dolor sit amet, consectetur hola?',
    answers: [
      {
        answer: 'Lorem ipsum dolor sit. 2',
        point: 150
      },
      {
        answer: 'Lorem ipsum dolor sit. 2.2',
        point: 220
      },
      {
        answer: 'Lorem ipsum dolor sit. 2.3',
        point: 330
      },
    ]
  },
  {
    question: '3Dorem orem ipsum dolor sit amet, consectetur hola?',
    answers: [
      {
        answer: 'Lorem ipsum dolor sit. 3',
        point: 180
      },
      {
        answer: 'Lorem ipsum dolor sit. 3.2',
        point: 230
      },
      {
        answer: 'Lorem ipsum dolor sit. 3.3',
        point: 270
      },
    ]
  },
])
</script>

<template>
  <div class="quiz">
    <h1 class="title">{{heroTitle}}</h1>
    <div class="quizBox">
      <div v-if="quizData.length !== 0">
        <template v-for="(item, i) in quizData">
          <h2 class="question">{{i+1}}. {{item.question}}</h2>
          <ul class="answerOptions" v-for="answer in item.answers">
            <li class="answerOption">{{answer.answer}}</li>
          </ul>
        </template>
      </div>
      <div v-else class="quizEmpty"><strong>Quiz is empty ):</strong></div>
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
  font-weight: 800;
  font-size: 34px;
  margin-top: 30px;
  margin-bottom: 30px;
}
.title{
  text-align: center;
}
h2{
  font-weight: 800;
  font-size: 28px;
  color: #ac2b3f;
}
.quizBox{
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  padding: 40px 35px;
  margin: 0 auto;
  max-width: 600px;
  min-height: 200px;
  background-color: #fff;
}
.quizEmpty{
  text-align: center;
  font-size: 20px;
}
.answerOptions{
  margin: 25px auto;
}
.answerOption{
  color: #ac2b3f;
  font-weight: 500;
  font-size: 20px;
  cursor: pointer;
}
.answerOption:not(:last-child){
  margin-bottom: 15px;
}
.answerOption.active{
  color: #ED2224;
}
.buttons{
  display: flex;
  justify-content: space-between;
  gap: 10px;
  padding: 20px 5px 0;
}
.btn{
  font-weight: 500;
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
  border-color: #ED2224;
  background-color: #fff;
}
</style>
