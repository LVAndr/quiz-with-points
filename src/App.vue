<script setup>
import {computed, ref} from "vue";

const heroTitle = 'Take the quiz, get a discount!';

const quizPoints = ref(0);
const discount = ref(0);
const quizData = ref([
  {
    question: ' Which chips flavor do you prefer?',
    options: [
      {
        answer: 'Cheese',
        point: 50,
        selected: false
      },
      {
        answer: 'Sour Cream & Onion',
        point: 60,
        selected: false
      },
      {
        answer: 'Barbecue',
        point: 70,
        selected: false
      },
    ]
  },
  {
    question: 'How often do you buy chips?',
    options: [
      {
        answer: 'Once a month',
        point: 100,
        selected: false
      },
      {
        answer: 'Once a week',
        point: 150,
        selected: false
      },
      {
        answer: 'Several times a week',
        point: 220,
        selected: false
      },
    ]
  },
  {
    question: 'What size of chips package do you usually choose?',
    options: [
      {
        answer: 'Small (up to 50g)',
        point: 130,
        selected: false
      },
      {
        answer: 'Medium (50-150g)',
        point: 190,
        selected: false
      },
      {
        answer: 'Large (over 150g)',
        point: 250,
        selected: false
      },
      {
        answer: 'Salt',
        point: 270,
        selected: false
      },
    ]
  },
]);
const getDiscount = () => {
  switch (true) {
    case (quizPoints.value >= 501):
      discount.value = 25;
      break;
    case (quizPoints.value > 400):
      discount.value = 15;
      break;
    case (quizPoints.value > 100):
      discount.value = 10;
      break;
    case (quizPoints.value > 0): // Тут охоплюються значення від 1 до 100
      discount.value = 5;
      break;
    default:
      discount.value = 0;
  }
  return discount.value;
};
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

const getCurrentQuestion = (item) => {
  quizData.value[activeIdx.value].options.forEach((option) => {
    if (option.selected === true){
      quizPoints.value-= option.point;
      option.selected = false;
    }
  })
  item.selected = true;
  quizPoints.value+= item.point;
  console.log(item)
  console.log('Points:', quizPoints.value)
};

const complete = ref(false);
const completeQuiz = computed(()=>{
  if (complete.value === false) complete.value = true;
})
const repeatQuiz = computed(()=>{
  if (complete.value === true) complete.value = false;
  activeIdx.value = 0;
  quizPoints.value = 0;
  for (let i = 0; i < quizData.value.length; i++) {
    quizData.value[i].options.forEach(option => {
      if (option.selected === true)option.selected = false;
    }
    )}
})

</script>

<template>
  <div class="quiz" v-if="!complete">
    <h1 class="title">{{heroTitle}}</h1>
    <div class="quizBox">
      <div v-if="quizData.length !== 0">
          <h2 class="question">{{activeIdx + 1}}. {{activeStep.question}}</h2>
          <ul class="answerOptions">
            <li
                :class="`answerOption ${
                  item.selected === true ? 'active' : ''
                }`"
                data-selected="false"
                v-for="(item, i) in activeStep.options"
                :key="i"
                @click="getCurrentQuestion(item)"
            >
              {{item.answer}}
            </li>
          </ul>
      </div>
      <div v-else class="quizEmpty"><strong>Quiz is empty ):</strong></div>
      <div class="buttons">
        <button class="btn" @click="prevStep" :disabled="prevDisabled">Previous</button>
        <button v-if="nextDisabled" class="btn" @click="completeQuiz; getDiscount()">Complete</button>
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
  width: 100%;
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
  display: block;
  padding: 8px 12px;
  color: #ac2b3f;
  font-weight: 500;
  font-size: 20px;
  cursor: pointer;
}
.answerOption:not(:last-child){
  margin-bottom: 15px;
}
.answerOption.active{
  background-color: #fff;
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
