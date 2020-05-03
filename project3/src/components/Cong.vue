<template>
  <div class="cong">
    
     <div class="title">
      <p class="h1-title">Congratulations!</p>
     
    </div>
    <div class="cong-1">
       
    </div>
  
  </div>
</template>
<script>

export default {
  name: 'Cong',
  components: {
    
  },
  data: () =>({
    
  }),
  methods: {
    

  
  },
  created: function () {
    
  }

}


</script>

<style scoped>
.cong{
  padding-top: 50px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
 .avatar-a {
   color: #CF87E9;
   font-size: 24px;
 }
 .avatar-b {
   color: #7DAEE9;
   font-size: 24px;
 }
 .avatar-c {
   color: #EDC494;
   font-size: 24px;
 }

 .avatar {
   display: flex;
   flex-direction: column;
   align-items: center;
   margin: 0px 25px 25px 40px;
 }

 .avatar img{
   width: 100px;
   height: 100px;
   margin-bottom: 24px;
 }

 .start-button{
  display: flex;
   flex-direction: column;
   align-items: center;
   margin-top: 60px;
 }

 .start-button button {
  background: #F9B623;
  border-radius: 8px;
  width: 300px;
  height: 56px;
  font-size: 24px;
  font-weight: bold;
  line-height: 29px;
  text-align: center;
  color: #FFFFFF;
  border: none;
  margin-top: 12px;

}
.cong-1 {
  display: flex;
  margin-top: 120px;
}

</style>
