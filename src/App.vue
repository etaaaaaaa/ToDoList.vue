<template>
  <!-- <div id="app"> -->
    <todolist></todolist>
  <!-- </div> -->
</template>

<script>
import Todolist from './components/Todolist.vue'

export default {
  name: 'App',
  components: {
    Todolist
  }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');
*{
  box-sizing: border-box;
  font-family: "Roboto";
  padding: 0;
  margin: 0;
  border: none;
}
body {
  padding: 0;
  margin: 0;
}
#app {
  overflow: hidden;
}
</style>
