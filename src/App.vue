<script setup>
import {computed, ref} from "vue";

const heroTitle = 'Take the quiz, get a discount!';

const quizPoints = ref(0);
const discount = ref(0);
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
]);
const activeIdx = ref(0);
const activeStep = computed(()=>{
  return quizData.value[activeIdx.value];
});

const nextStep = computed(()=>{
  if (activeIdx.value !== quizData.value.length - 1){
    activeIdx.value++
  }
});
const prevStep = computed(()=>{
  if (activeIdx.value !== 0)activeIdx.value--;
});

const prevDisabled = computed(()=>{
  return activeIdx.value === 0;
})
const nextDisabled = computed(()=>{
  return activeIdx.value === quizData.value.length - 1;
});

const complete = ref(false);
const completeQuiz = computed(()=>{
  if (complete.value === false) complete.value = true;
})
const repeatQuiz = computed(()=>{
  if (complete.value === true) complete.value = false;
  activeIdx.value = 0;
})
</script>

<template>
  <div class="quiz" v-if="!complete">
    <h1 class="title">{{heroTitle}}</h1>
    <div class="quizBox">
      <div v-if="quizData.length !== 0">
          <h2 class="question">{{activeIdx + 1}}. {{activeStep.question}}</h2>
          <ul class="answerOptions" v-for="(item, i) in activeStep.answers" :key="i">
            <li class="answerOption">{{item.answer}}</li>
          </ul>
      </div>
      <div v-else class="quizEmpty"><strong>Quiz is empty ):</strong></div>
      <div class="buttons">
        <button class="btn" @click="prevStep" :disabled="prevDisabled">Previous</button>
        <button class="btn">Submit</button>
        <button v-if="nextDisabled" class="btn" @click="completeQuiz">Complete</button>
        <button v-else class="btn" @click="nextStep">Next</button>
      </div>
    </div>
  </div>
  <div class="quiz" v-else>
    <h1 class="title">Quiz is complete!</h1>
    <div class="quizBox">
      <strong>Your points: {{quizPoints}}</strong>
      <strong>Your discount: {{discount}}%</strong>
      <div class="buttons">
        <button class="btn" @click="repeatQuiz">Repeat</button>
      </div>
    </div>

  </div>
</template>

<style scoped>
h1{
  font-weight: 800;
  font-size: 34px;
  margin-top: 30px;
  margin-bottom: 60px;
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
  background-color: #b9c0cb;
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
  min-width: 110px;
  padding: 8px 14px;
  border: 1px solid #210404;
  border-radius: 18px;
  transition: all .2s;
}
.btn:disabled{
  border: 1px solid #858585;
  color: #858585;
}
.btn:disabled:hover{
  background-color: transparent;
}
.btn:disabled:active{
  color: #858585;
  border-color: #858585;
  cursor: default;
}
.btn:hover{
  background-color: #fff;
}
.btn:active{
  color: #ED2224;
  border-color: #ED2224;
}
</style>
