<template>
  <div class="home">
    <Quiz v-on:get-feedback="setResult" v-if="stage=='quiz'"></Quiz>
    <Feedback :result="result" v-if="stage=='feedback'"></Feedback>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import Quiz from '@/components/Quiz.vue'
import Feedback from '@/components/Feedback.vue'

export default {
  name: 'Home',
  components: {
    Quiz,
    Feedback
  },
  data: () =>({
    result:[],
    stage: "quiz"
  }),
  methods: {
    setResult: function (_r) {
      this.result = _r;
      this.stage = "feedback"
    }
  }
}
</script>
