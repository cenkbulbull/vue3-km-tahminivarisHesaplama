<template>
  <div class="container">
    <div>
      <h3 class="flow-text">Gideceğiniz yere tahmini varış süresini hesaplayın...</h3>
      <button @click="$router.push({name:'calc'})" class="waves-effect waves-light btn-small">Başla</button>
    </div>
  </div>
</template>

<script>
  export default {

  }
</script>
<style>
  .container{
    width: 100%;
    height: 100vh;
    text-align: center;    
    overflow: hidden;
  }
  .container div{
    margin-top: 250px !important;
  }
  .container div .flow-text{
    margin-bottom: 20px !important;
  }
</style>