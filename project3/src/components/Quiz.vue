<template>
  <div class="quiz">
   
      <div class="title">
        <p class="h1-title">Quiz <span>{{round_count}}</span> </p>
      </div>
      <div class="quiz-area">
        <div class="qa-i" v-for="(item, idx) in quiz_data" :key="idx">
          <p>{{item.question}}</p>
          <div class="qai-i">
            <input type="radio" :value="item.choices[0].is_right" v-model="learner_result[idx]"> 
            <label>{{item.choices[0].content}}</label>
          </div>
          <div class="qai-i">
            <input type="radio" :value="item.choices[1].is_right" v-model="learner_result[idx]"> 
            <label>{{item.choices[1].content}}</label>
          </div>
          <div class="qai-i">
            <input type="radio" :value="item.choices[2].is_right" v-model="learner_result[idx]"> 
            <label>{{item.choices[2].content}}</label>
          </div>
          <div class="qai-i">
            <input type="radio" :value="item.choices[3].is_right" v-model="learner_result[idx]"> 
            <label>{{item.choices[3].content}}</label>
          </div>
         
        </div>
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
  name: 'Quiz',
  components: {

  },
  data: () =>({
    round_count: 1,
    quiz_data: [],
    learner_result: [],
    if_new_round: [true, true, true, true],
    
  }),
  methods: {
    shuffle: function (array) {
      array.sort(() => Math.random() - 0.5);
    },
    generate_questions: function () {
      const raw_data = require("@/assets/question.json");
      for(var i = 0  ; i < 4; i ++){
        //pick the right answers
        var item_right_answers = raw_data.data[i].right_answers; 
        var right_idx = Math.floor(Math.random()* item_right_answers.length )
        var the_right_answer = {
          content:item_right_answers[right_idx],
          is_right: true
        };

        //pick the wrong answers
        var item_wrong_answers = raw_data.data[i].wrong_answers; 
        this.shuffle(item_wrong_answers);
        var the_wrong_answers = item_wrong_answers.slice(0, 3)
        the_wrong_answers = the_wrong_answers.map(e=>({
          content: e,
          is_right: -1*Math.random()
        }))

        //shuffle choices
        var temp_choices = [the_right_answer, ...the_wrong_answers]
        this.shuffle(temp_choices)


        //add generated questions into quiz_data
        var item = {
          "question":raw_data.data[i].question,
          "choices": temp_choices
        }

        this.quiz_data.push(item);

      }
    },
    assessQuiz: function () {
      for(var i = 0; i < 4 ; i ++ ) {
      
        if(this.learner_result[i] !== true){
          this.if_new_round[i] = false;
        }
      }
      console.log(this.if_new_round);
    }
  },
  created: function () {
    this.generate_questions();

  }
}
</script>
