<template>
  <div class="myHeader">
    <span class='title'>娜娜原创</span>
  </div>
</template>

<script>
export default {
  name: 'myHeader'
}
</script>

<style scoped>
@-webkit-keyframes mymove {
    50% {box-shadow: 10px 20px 30px blue;}
}
/* Standard syntax */
@keyframes mymove {
    50% {box-shadow: 10px 20px 30px blue;}
}

.title {
  font-size: 28px;
  color: #FFFFFB;
    background-color: transparent;
    text-shadow: 0 0 20px #fdec84,
          10px -10px 30px #ffae35,
          20px -20px 40px #ec760c,
          -20px -60px 50px #cd4607,
          0px -80px 60px #973717,
          10px -40px 70px #451b0e;
  animation: mymove;
  -webkit-animation: mymove 5s infinite;
}


</style>