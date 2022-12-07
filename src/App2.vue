<template>
    <h1>ONLINE TESTS</h1>

    <div class="container">
        <div class="tests">

            <div class="test"
                 :class="{hidden: show == true}"
                 v-for="test in tests">

                <img src="./assets/totem.png" class="test_img">
                <div class="test_text">
                    <p class="title" 
                       @click="currentTest = test; currentQuest = test.questions; currentAnswersWithDesc = test.answersWithDesc; show = true">{{test.title}}</p>
                    <p class="disc">
                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. 
                        Unde error velit quibusdam accusantium, 
                        perferendis ab totam numquam reiciendis ad optio.
                    </p>
                </div>
                
                <span>Selected: {{ picked }}</span> -->

                
            </div>   

        </div>
    </div>
    <!-- <div class="container">
        <div class="questions">
            <div class="question">
                <p>Question: 1/10</p>
                <div class="question_header">{{}}</div>
                <img src="./assets/nice_cat.png" class="question_img">
                <div class="answers">
                    <label for="myRadioId" class="radio">
                        <input type="radio" name="myRadioField" id="myRadioId" class="input_radio">
                        <div class="radio_radio"></div>
                        Lorem ipsum dolor sit.
                    </label>
                    <label for="myRadioId2" class="radio correct">
                        <input type="radio" name="myRadioField" id="myRadioId2" class="input_radio">
                        <div class="radio_radio correct"></div>
                        Lorem, ipsum dolor.
                    </label>
                    <label for="myRadioId3" class="radio incorrect">
                        <input type="radio" name="myRadioField" id="myRadioId3" class="input_radio">
                        <div class="radio_radio incorrect"></div>
                        Lorem ipsum dolor sit amet.
                    </label>
                </div>
                <div class="correct"> Correct! / Incorrect. </div>
                <button>Next</button>
            </div>
        </div>
    </div> -->
    <TestCard :class="{hidden: show == false}"
              :test="currentTest"
              :questions="currentQuest"
              :descs="currentAnswersWithDesc"
              :imgs="tests[0].answersImgs"
              :values="!tests[0].correctAnswers ? tests[0].questions[0].variants.map(va => va.value) : 'none'"/>

</template>

<script>
import TestCard from './components(2)/TestCard.vue'

export default {
  name: 'App2',
  data() {
    return {
        picked: '',
        currentTest: '',
        currentQuest: '',
        currentAnswersWithDesc: '',
        show: false,
        tests: [{
            title: 'What is your totem animal?',
            numberOfQuestions: 5,
            correctAnswers: false,
            answersWithDesc: {
                dolphin: 'DOLPHIN DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.',
                dog: 'DOG DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.',
                cat: 'CAT DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.',
                rabbit: 'RABBIT DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.',
                bear: 'BEAR DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.',
            },
            answersImgs: {
                ///img/dolphin.8f0fbf5e.png /img/nice_cat.c3b362a7.png /img/nice_cat.c3b362a7.png /img/rabbit.bdba4e38.png /img/bear.44ce2793.png
                dolphin: '/img/dolphin.8f0fbf5e.png',
                dog: '/img/dog.73609e0c.png',
                cat: '/img/nice_cat.c3b362a7.png',
                rabbit: '/img/rabbit.bdba4e38.png',
                bear: '/img/bear.44ce2793.png',
            },
            questions: [{
                num: 1,
                question: 'Pick a color',
                variants: [{
                    color: 'blue',
                    value: 'dolphin',
                    description: 'DOLPHIN DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.'
                },{
                    color: 'green',
                    value: 'dog',
                    description: 'DOG DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.'
                },{
                    color: 'red',
                    value: 'cat',
                    description: 'CAT DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.'
                },{
                    color: 'yellow',
                    value: 'rabbit',
                    description: 'RABBIT DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.'
                },{
                    color: 'black',
                    value: 'bear',
                    description: 'BEAR DESCRIPTION: Lorem ipsum dolor sit amet, consectetur adipisicing elit. Unde error velit quibusdam accusantium, perferendis ab totam numquam reiciendis ad optio.'
                }],
                img: '/img/T1_Q1.11227e93.jpg'  
            },{
                num: 2,
                question: 'Pick a vacation place',
                variants: [{
                    color: 'seaside',
                    value: 'dolphin'
                },{
                    color: 'countryside',
                    value: 'dog'
                },{
                    color: 'city',
                    value: 'cat'
                },{
                    color: 'flower field',
                    value: 'rabbit'
                },{
                    color: 'forest',
                    value: 'bear'
                }]   ,
                img: '/img/T1_Q2.d349c678.jpg'   
            },{
                num: 3,
                question: 'What do you like in people?',
                variants: [{
                    color: 'smartness',
                    value: 'dolphin'
                },{
                    color: 'loyalty',
                    value: 'dog'
                },{
                    color: 'independance',
                    value: 'cat'
                },{
                    color: 'kindness',
                    value: 'rabbit'
                },{
                    color: 'honesty',
                    value: 'bear'
                }],
                img: '/img/T1_Q3.fed92fc8.jpg '
            },{
                num: 4,
                question: 'What is your favorite food?',
                variants: [{
                    color: 'seafood',
                    value: 'dolphin'
                },{
                    color: 'an ice-cream',
                    value: 'dog'
                },{
                    color: 'a gourman dish',
                    value: 'cat'
                },{
                    color: 'a vegetable salad',
                    value: 'rabbit'
                },{
                    color: 'a beef steak',
                    value: 'bear'
                }]  ,
                img: '/img/T1_Q4.de083665.jpg ' 
            },{
                num: 5,
                question: 'What is your favorite school subjuct?',
                variants: [{
                    color: 'Arts&Crafts',
                    value: 'dolphin'
                },{
                    color: 'Math',
                    value: 'dog'
                },{
                    color: 'Science',
                    value: 'cat'
                },{
                    color: 'Literature',
                    value: 'rabbit'
                },{
                    color: 'PE',
                    value: 'bear'
                }]  ,
                img: '/img/T1_Q5.585135ac.jpg '
            }]
      }]
    } 
  },
  components: {
    TestCard
  }
}

</script>

<style>
#app2 {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}
.tests {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.test {
  width: 340px;
  margin: 10px;
  position: relative;
  background: #fff;
}

.test_img {
  width: 340px; 
}

p.title {
  font-size: 30px;
  text-decoration: none;
  color: #2c3e50;
  line-height: 1;
  font-weight: 500;
  cursor: pointer;
}

p.title:hover {
    text-shadow: 0px 0px 3px #7b838b;
}

.disc {
    position: relative;
    top: -13px;
}

.questions {
    display: flex;
    justify-content: center;
    align-items: center;
    background: #fff;
    height: 800px;
    width: 600px;
    margin-left: 200px;
    overflow: hidden;
}

.question_header {
    font-size: 30px;
    /* border: 1px solid red; */
    margin-top: 10px;
    margin-bottom: 10px;
    width: 780px;
    background: #f2dbcf8c;
}

.question_img {
    width: 600px;
}

.answers {
    text-align: left;
    width: 600px;
    margin-left: 90px;
    margin-top: -15px;
    background: #f2dbcf8c;
    padding: 16px 10px 10px 10px;
    display: flex;
    flex-direction: column;
}

.input_div {
    margin-top: 4px;
    /* margin-bottom: 20px; */
    background: #fff;
    line-height: 3;
    border-radius: 5px;
}

/* =============================== */

.radio {
    display: inline-flex;
    align-items: center;
    cursor: pointer;
    background: #ffffff;
    margin: 4px 0px;
    padding: 8px;
    border-radius: 5px;
}

/* .input_radio {
    /* display: none; 
} */

.radio_radio {
    width: 1.25em;
    height: 1.25em;
    border: 1px solid #7d7b7bef;
    border-radius: 10%;
    margin-right: 10px;
    box-sizing: border-box;
    padding: 2px;
    overflow: hidden;
}

.radio_radio::after {
    content: "\2612";
    width: 100%;
    height: 100%;
    display: block;
    border-radius: 10%;

    transform: scale(2.4);
    margin-top: -11px;
    margin-left: 2px;
    margin-bottom: 5px;
    opacity: 0;
    transition: opacity 0.15s;
} 

.input_radio:checked + .radio_radio::after {
    opacity: 1;
}

/* .correct {
    background: rgb(222, 255, 192);
}

.radio_radio.correct::after  {
    content: "\2611";
    opacity: 1;
    color: #317705;
}

.radio_radio.correct {
    border: 1px solid #317705;
} */

/* ==== */

/* .incorrect {
    background: rgb(255, 192, 192);
}

.radio_radio.incorrect::after  {
    content: "\2612";
    opacity: 1;
    color: #b50000;
}

.radio_radio.incorrect {
    border: 1px solid #b50000;
} */

.hidden  {
    display: none;
}


</style>