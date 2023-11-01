<template>
  <div class="main">
    <div class="titleContainer">
      <div class="title">KOMONA</div>
      <div class="prod">PRODUCTION</div>
    </div>
  </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>

  .main {
    background-color: black;
    height: 100vh;

    .titleContainer {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      .title {
        font-family: 'lovelo';
        color: white;

        text-transform: capitalize;
        font-size: 10rem;
        text-align: enter;
      }

      .prod {
        font-family: 'balgin';
        color: #FFFFFF;
        font-size: 4rem;
        letter-spacing: 1rem;
        margin-top: -1.2rem;
        text-align: center;
      }
    } 
  }
</style>

