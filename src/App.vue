<template>
  <div id="app">
    <h1 class="heading">STOP WATCH     <b-icon font-scale="1.8" icon="stopwatch-fill" animation="cylon" ></b-icon> </h1>
  <div class="content">
    <StopWatch/>
  </div>
  </div>
  
</template>

<script>
import StopWatch from './components/Stopwatch.vue'

export default {
  name: 'App',
  components: {
    StopWatch
  }
}
</script>

<style>
.heading{
    color: aliceblue;
    padding-top:120px ;
  }
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #3a546e;
  background-color: #151238;
  width: 100vw;
  height: 100vh;
}
.content{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 65%;
}
</style>
