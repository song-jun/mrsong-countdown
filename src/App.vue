<template>
  <div id="app">
    <mrsong-countdown @sendData='getData' :isYear='false'>
      <!-- <div>{{time.timeText}}</div> -->
    </mrsong-countdown>
  </div>
</template>

<script>
  import mrsongCountdown from '../src/myPlugin/mrsongCountdown/mrsong-countdown'; // 引入
  export default {
    name: 'app',
    data() {
      return {
        msg: 'Welcome to Your Vue.js App',
        time:{
          timeText:null
        },
      }
    },
    components: {
      mrsongCountdown
    },
    methods:{
      getData(e){
        console.log(e);
        this.time=e;
      }
    }
  }
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  h1,
  h2 {
    font-weight: normal;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
