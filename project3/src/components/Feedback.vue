<template>
  <div class="feedback">
   
      <div class="title">
        <p class="h1-title">Feedback </p>
      </div>
      <div v-if="!no_score">
        <p>score</p>
        <p>{{score}}</p>
      </div>
       <div class="quiz-area">
          <div class="qa-i" v-for="(item, idx) in quiz_data" :key="`${idx}_1`" >
            <div v-if="show_result[idx]">
              <p>{{item.question}}</p>
              <div class="qai-i">
                <input type="radio" :value="item.choices[0].is_right" disabled v-model="learner_result[idx]" > 
                <label v-bind:class="{right_answer:(item.choices[0].is_right == true)}">{{item.choices[0].content}}</label>
              </div>
              <div class="qai-i">
                <input type="radio" :value="item.choices[1].is_right" disabled v-model="learner_result[idx]"> 
                <label  v-bind:class="{right_answer:(item.choices[1].is_right  == true)}">{{item.choices[1].content}}</label>
              </div>
              <div class="qai-i">
                <input type="radio" :value="item.choices[2].is_right" disabled v-model="learner_result[idx]"> 
                <label v-bind:class="{right_answer:(item.choices[2].is_right  == true)}">{{item.choices[2].content}}</label>
              </div>
              <div class="qai-i">
                <input type="radio" :value="item.choices[3].is_right" disabled v-model="learner_result[idx]" > 
                <label v-bind:class="{right_answer:(item.choices[3].is_right  == true)}">{{item.choices[3].content}}</label>
              </div>
              <div class="feedback-i">
                  <p><span v-if="!result[idx]">Correct!</span> 
                      <span v-if="result[idx]">Not quite right!</span>
                      This is explanation!!!!</p>
              </div>
            
            </div>
          </div>
          <div class="ma-i" v-for="(item, idx) in mul_quiz_data" :key="`${idx}_2`" >
          <div v-if="show_result[idx+2]">
            <p>{{idx+3}} . {{item.question}}</p>
            <div class="mai-i">
              <input type="checkbox" :value="item.choices[0].is_right" v-model="learner_result_2[idx]" disabled> 
              <label v-bind:class="{right_answer:(item.choices[0].is_right != 0)}">{{item.choices[0].content}}</label>
            </div>
            <div class="mai-i">
              <input type="checkbox" :value="item.choices[1].is_right" v-model="learner_result_2[idx]" disabled> 
              <label v-bind:class="{right_answer:(item.choices[1].is_right != 0)}">{{item.choices[1].content}}</label>
            </div>
            <div class="mai-i">
              <input type="checkbox" :value="item.choices[2].is_right" v-model="learner_result_2[idx]" disabled> 
              <label v-bind:class="{right_answer:(item.choices[2].is_right != 0)}">{{item.choices[2].content}}</label>
            </div>
            <div class="mai-i">
              <input type="checkbox" :value="item.choices[3].is_right" v-model="learner_result_2[idx]" disabled> 
              <label v-bind:class="{right_answer:(item.choices[3].is_right != 0)}">{{item.choices[3].content}}</label>
            </div>
            <div class="feedback-i">
                  <p><span v-if="!result[idx+2]">Correct!</span> 
                      <span v-if="result[idx+2]">Not quite right!</span>
                      This is explanation!!!!</p>
              </div>
          </div>
        </div>
       </div>
       
      <div class="feedback-area">
        
      </div>
      <button class="cp-btn" @click="after_feedback()">Done</button>
     
   

  </div>
</template>

<style scoped>
.feedback {
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

.qai-i, .mai-i {
  display: flex;
  margin-bottom: 24px;
  
}

label {
  text-align: left;
}

.right_answer {
  color: #FFC107;
  font-weight: 600;
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

  .feedback-i{
    background-color: #eee;
    padding: 12px;
  }

</style>

<script>

  export default {
    name: 'Feedback',
    components: {

    },
    props:["result","quiz_data","learner_result", "show_result", "no_score","mul_quiz_data", "learner_result_2"],
    data: () =>({
      points: 0,
      score: 0,
      
      
    }),
    methods: {
      calculate_score: function () {
        // console.log(this.result)
        for(var i = 0; i < this.result.length; i++)
        {
          if(!this.result[i]){
            this.points++;
          }
        }
        this.score = Math.ceil((this.points / this.result.length)*100)
      },
      after_feedback: function () {
        this.$emit("after-feedback",this.result);
        
      }
      
    },
    created: function () {
      this.calculate_score();

    }
  }
</script>
