<template>
  <v-app>
    <div class="bg">

      <v-main>
        <v-container >
        <nuxt/>
        </v-container>
      </v-main>
    </div>
    <div class="overlay ">
      </div>
  </v-app>
</template>
<style lang="scss" scoped>
  .bg{
    height: 100vh;
    width: 100%;
    position: absolute;
    background-image: url('../static/assets/bg-lagos.jpg');
  }
  .overlay{
    height: 100vh;
    width: 100%;
    background-color: #37444e;
    position: relative;
    opacity: 0.6;
    
  }
</style>
