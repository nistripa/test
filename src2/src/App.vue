<template>
  <div id="app">
    <SubjectList/>
      <div class="title">
      {{question.title}}
      </div>
      <div v-if="submitted" style="text-align: right">
      Total: {{ total }}
      </div>
      <br><br>

    <div class="question" v-for="(q, index) in question.questions" :key="index">
      <div> {{q.id}}: {{q.text}}</div>
      
      <div v-for="a in q.values" :key="a">
        <input type="radio" :name="q.id" id="a" :value="a" @click="checkrightAnswer(a, q.correctAnswer, index)">
        <label :for="a">{{a}}</label>
      </div>      
          <div v-if="submitted && result[index] === 0"><img class="image" src="./img/delete.jpg"></div>
          <div v-if="submitted && result[index] === 1"><img class="image" src="./img/tick.png"></div>
          <br><br>
    </div>
    <br><br>
    <button @click="SumArray">submit</button>

  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import { mathsquestions } from './data/mathsquestions.js'

import { result } from './data/result.js'
// import SubjectList from './components/SubjectList.vue'
import SubjectList from './components/SubjectList'



export default {
  name: 'App',
  components: {
    // HelloWorld
    SubjectList
  },
  data() {
    return {
      question: mathsquestions,
      result : result,
      correct:'',
      total:0,
      submitted : false
    }
  },
  methods: {
    checkrightAnswer(id, a, index){

      if (id === a)
      {
        console.log(result);
        result[index] = 1;
        console.log(result);
        this.correct = 'correct'
      }
      else{
        console.log(result);
        result[index] = 0;
        console.log(result);
        this.correct = 'correct'
      }
    },
SumArray(){
        this.submitted = true;
        this.total = 0;
  var output;
  output = result.reduce(function(total, num){ 
    return total + num;
  } , 0); 
  console.log(output)
  this.total = output;
  
}
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.question{
  text-align: left;
}
.title{
  font-weight: bolder;
  font-size: 40px;
}
.image{
  height: 30px;
  width: 50px;
}
option {
  margin: 0.5em;
}
</style>
