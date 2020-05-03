<template>
  <div class="quiz">
   
      <div class="title">
        <p class="h1-title">Quiz <span>{{round_count}}</span> </p>
      </div>
      <div class="quiz-area">
        <div class="qa-i" v-for="(item, idx) in quiz_data" :key="`${idx}_3`" >
          <div v-if="if_new_round[idx]">
            <p>{{idx+1}} . {{item.question}}</p>
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
        <div class="ma-i" v-for="(item, idx) in mul_quiz_data" :key="`${idx}_4`" >
          <div v-if="if_new_round[idx+2]">
            <p>{{idx+3}} . {{item.question}}</p>
            <div class="mai-i">
              <input type="checkbox" :value="item.choices[0].is_right" v-model="learner_result_2[idx]"> 
              <label>{{item.choices[0].content}}</label>
            </div>
            <div class="mai-i">
              <input type="checkbox" :value="item.choices[1].is_right" v-model="learner_result_2[idx]"> 
              <label>{{item.choices[1].content}}</label>
            </div>
            <div class="mai-i">
              <input type="checkbox" :value="item.choices[2].is_right" v-model="learner_result_2[idx]"> 
              <label>{{item.choices[2].content}}</label>
            </div>
            <div class="mai-i">
              <input type="checkbox" :value="item.choices[3].is_right" v-model="learner_result_2[idx]"> 
              <label>{{item.choices[3].content}}</label>
            </div>
          </div>
        </div>
      </div>
      <button class="cp-btn" @click="assessQuiz()">Submit</button>
     
   

  </div>
</template>

<style scoped>
.quiz {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.quiz-area {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 50%;
}
.qa-i, .ma-i {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 24px;
}

.qa-i p,
.ma-i p {
  font-weight: bold;
  text-align: left;
}

.qai-i,
.mai-i {
  display: flex;
  margin-bottom: 24px;
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
    mul_quiz_data: [],
    learner_result: [],
    learner_result_2: [[],[]],
    if_new_round: [true, true, true, true],
    
  }),
  props: ["question_select"],
  methods: {
    shuffle: function (array) {
      array.sort(() => Math.random() - 0.5);
    },
    generate_questions: function () {
      const single_raw_data = require("@/assets/source_question.json");
      const mul_raw_data = require("@/assets/mc_questions.json");
      
      for(var i = 0  ; i < 2; i ++){
        //pick the right answers
        var item_right_answers = single_raw_data.data[i].right_answers; 
        var right_idx = Math.floor(Math.random()* item_right_answers.length )
        var the_right_answer = {
          content:item_right_answers[right_idx],
          is_right: true
        };

        //pick the wrong answers
        var item_wrong_answers = single_raw_data.data[i].wrong_answers; 
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
          "question":  single_raw_data.data[i].question,
          "choices": temp_choices
        }

        this.quiz_data.push(item);

      }
      for(var i = 0  ; i < 2; i ++){
        //pick the wrong answers
        var item_wrong_answers = mul_raw_data.data[i].wrong_answers; 
        var wrong_idx = Math.floor(Math.random()* item_wrong_answers.length )
        
        var the_wrong_answer = {
          content:item_wrong_answers[wrong_idx],
          is_right: 0
        };

        //pick the right answers
        var item_right_answers = mul_raw_data.data[i].right_answers; 
        this.shuffle(item_right_answers);
        var the_right_answers = item_right_answers.slice(0, 3)
        var final_right_items = []
        for(var j =0 ; j<3; j++){
          var _a = {
            content: the_right_answers[j],
            is_right: j+1
          }
          final_right_items.push(_a)
        }
    

        //shuffle choices
        var temp_choices = [the_wrong_answer, ...final_right_items]
        this.shuffle(temp_choices)


        //add generated questions into mul_quiz_data
        var item = {
          "question": mul_raw_data.data[i].question,
          "choices": temp_choices
        }

        this.mul_quiz_data.push(item);

      }
    },
    assessQuiz: function () {
      for(var i = 0; i < 2 ; i ++ ) {
      
        if(this.learner_result[i] === true){
          //if answer is right, do not show the question
          //this.if_new_round[i] = false;
          this.$set(this.if_new_round,i,false)

        }
      }

      //assess multiple choice
      for(var i = 0; i < 2 ; i ++) {
        
        var is_wrong;
        for(var j = 0; j < this.learner_result_2[i].length; j++)
        {
          if(this.learner_result_2[i][j] == 0){
           
            is_wrong = true;
          }

         
        }
        if(this.learner_result_2[i].length == 3 && !is_wrong){
          this.$set(this.if_new_round,i+2,false)
        }else{
          break;
        }

      }
      this.$emit("get-feedback",[this.if_new_round, this.quiz_data, this.learner_result, this.mul_quiz_data, this.learner_result_2]);
      
    },
    set_if_new: function () {
      if(this.question_select.length != 0)
      {
        
        this.if_new_round = this.question_select;
      }
    }
  },
  created: function () {
    this.generate_questions();
    this.set_if_new()

  }
}
</script>
