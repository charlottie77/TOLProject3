<template>
  <div class="home">
    <Quiz v-on:get-feedback="setResult" :question_select="result" v-if="stage=='quiz'"></Quiz>
    <Feedback v-on:after-feedback="nextStep" :result="result" :quiz_data="quiz_data" 
              :learner_result="learner_result" :show_result="temp_result" :no_score="no_score"
              :mul_quiz_data="mul_quiz_data" :learner_result_2="learner_result_2" v-if="stage=='feedback'"></Feedback>
    <Cong v-if="stage=='cong'"></Cong>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import Quiz from '@/components/Quiz.vue'
import Feedback from '@/components/Feedback.vue'
import Cong from '@/components/Cong.vue'

export default {
  name: 'Home',
  components: {
    Quiz,
    Feedback,
    Cong
  },
  data: () =>({
    result:[],
    stage: "quiz",
    quiz_data: [],
    mul_quiz_data: [],
    learner_result: [],
    learner_result_2: [],
    temp_result: [true, true, true, true],
    no_score: false,
  }),
  methods: {
    setResult: function (_r) {
     
      [this.result, this.quiz_data, this.learner_result, this.mul_quiz_data, this.learner_result_2] = _r;
      this.stage = "feedback"
    },
    nextStep: function (_r) {
      console.log("wdnmd")
      for(var i = 0 ; i < 4 ; i ++) {
        if(_r[i]){
          this.result = _r;
          this.stage = "quiz"
          break;
        }
        else{
          this.stage = "cong"
        }
      }
       this.temp_result = [...this.result];
       this.no_score = true;
    }
  }
}
</script>
