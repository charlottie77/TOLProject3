<template>
  <div class="feedback">
   
      <div class="title">
        <p class="h1-title">Feedback </p>
      </div>
      <div>
        <p>score</p>
        <p>{{result}}</p>
      </div>
      <div class="feedback-area">
        
      </div>
      <button class="cp-btn" @click="assessQuiz()">Done</button>
     
   

  </div>
</template>

<style scoped>
.quiz-area {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 50%;
}
.qa-i {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 24px;
}

.qa-i p {
  font-weight: bold;
  text-align: left;
}

.qai-i {
  display: flex;
  
}

label {
  text-align: left;
}


.cp-btn {
    background: #F9B623;
    border-radius: 8px;
    width: 166px;
    height: 56px;
    font-size: 24px;
    font-weight: bold;
    line-height: 29px;
    text-align: center;
    color: #FFFFFF;
    border: none;
    margin-top: 60px;
  }

</style>

<script>
//import question_data from "@/assets/question.json"

export default {
  name: 'Feedback',
  components: {

  },
  props:["result"],
  data: () =>({
    
    
  }),
  methods: {
    
  },
  created: function () {
    

  }
}
</script>
