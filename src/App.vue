<template>
  <div id="app">
    <date-time />   
  </div>
</template>

<script>
import DateTime from './components/DateTime'

export default {
  name: 'app',
  components: {
    DateTime
  }
}
</script>

<style>
@import url('//cdn.jsdelivr.net/font-iropke-batang/1.2/font-iropke-batang.css');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-weight: lighter;
}

#app {
  width: 100vw;
  height: 100vh;
  background-color: #3a3b3c;
  color: #f1f1f1;
  font-family: 'Iropke Batang', Helvetica, Arial, sans-serif;
}

h1{
  font-size: 3rem;
}
</style>
