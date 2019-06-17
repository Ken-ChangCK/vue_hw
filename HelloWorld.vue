<template>
  <div class="hello">
    <!-- <link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous"> -->
    <div class="nav">
      <div class="col-md-11 col-md-offset-4"><h2 > 資管金頭腦</h2><hr>
       <h5><div class="score">Your Score: {{numCorrect}}/{{numTotal}} </div></h5></div>
  </div>   
  </div> 
</template>

<script>

export default {
  name: 'HelloWorld',
  props: ['numTotal','numCorrect'],
  watch: {
      numTotal : {
        immediate: true,
      }
  }
}
</script>

<style scoped>
.nav {
        height: 50px;
        background-color: lightgrey;
        text-align: center;
        line-height:100px;
  
      }
.score {
  color: rgb(47, 51, 255);
  text-align: center;

}
.Hello{
  text-align: center;  
}

</style>
