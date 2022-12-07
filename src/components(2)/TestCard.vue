<template>

     <div class="container">
            
        <div class="questions"
             :class="{hidden2: show2 == true}">
            <div class="wrapper"
                 :style="{ 'top': moveTo}">
                <div class="question"
                    v-for="quest, i of test.questions"
                    >

                    <div class="myDiv">
                        {{quest.question}}
                        <div class="myDiv">{{quest.num}}</div>
                        <div class="myDiv"
                            v-for="va in quest.variants"
                            style="height: 40px;">
                            {{va.color}}
                        </div>
                    </div>
                    
                    <p>Question: {{quest.num}} / {{test.numberOfQuestions}} </p>
                    <div class="question_header">{{ quest.question}}</div>
                    <img :src="quest.img" class="question_img" style="height: 400px;">
                    <div class="answers">
                        <label :for="variant.color + j" 
                               class="radio"
                               v-for="variant, j in quest.variants">

                            <input type="radio" 
                                   :name="i" 
                                   :id="variant.color + j" 
                                   v-model="picked"
                                   :value="variant.value"
                                   class="input_radio">

                            <div class="radio_radio"></div>
                            {{variant.color}}
                        </label>
                    </div>
                    <!-- <span>Selected: {{ picked }}</span> -->
                    <!-- <div class="correct"> Correct! / Incorrect. </div> -->
                    <button @click="i == questions.length - 1 ? getResults(picked) : moveTo = tops[i+1]; ansArr.push(picked)">
                            {{btn}}
                    </button>
                </div>
            </div>
        </div>
        <ResultCard :class="{hidden2: show2 == false}"
                    :animal="animal"/>
    </div>
</template>

<script>
import ResultCard from './ResultCard.vue'

    export default {
        
        name: 'TestCard',
        props: ['test', 'questions', 'values', 'descs', 'imgs'],
        components: {
            ResultCard
        },
        data() {
            return {
                picked: '',
                show2: false,
                animal: {
                    name: '',
                    desc: '',
                    img: ''
                },
                btn: 'Next',
                result: '',
                ansArr: [],
                moveTo: '1760px',
                tops: ['1760px', '840px', '-90px', '-1000px', '-1930px'] ,
            }
        },
        methods: {
            createValCounters(val) {
                this.ansArr.push({
                    name: val,
                    counter: 0
                })
            },
            getResults(picked) {
                this.btn = 'Result'
                this.result = this.ansArr.reduce(function(acc, el) {
                    acc[el] = (acc[el] || 0) + 1;
                    return acc;
                }, {});
                console.log(this.result);

                let numArray = []
                let num = 0
                //let animal = ''
                for (let key in this.result) {
                    num > this.result[key] ? num = num : num = this.result[key]
                }
                this.animal.name = Object.keys(this.result).find(key => this.result[key] === num)
                this.animal.desc = this.descs[this.animal.name]
                this.animal.img = this.imgs[this.animal.name]
                
                this.show2 = true
                console.log(num, this.animal.name, this.animal.desc);
            }
        }
        
    }
</script>

<style scoped>
.myDiv {
    width: 100px;
    height: 150px;
    color: #fff;
    background: black;
    overflow: visible;
}

.wrapper {
    position: relative;
    left: -10px;
    top: 1760px;
    /* top: 840px;
    top: -90px;
    top: -1000px;
    top: -1930px; */
}

.radio {
    display: inline-flex;
    align-items: center;
    cursor: pointer;
    background: #ffffff;
    margin: 4px 0px;
    padding: 8px;
    border-radius: 5px;
}

.input_radio {
     display: none; 
}

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

.hidden2  {
    display: none;
}
</style>