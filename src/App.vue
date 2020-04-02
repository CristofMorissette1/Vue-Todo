<template>
  <div id="app">

  </div>
</template>

<script>


export default {
  name: 'App',
  components: {

  },
  data() {
    return {
      Todos: [
        {
          id: 1,
          title: "My first Todo",
          completed: false
        },
        {
          id: 2,
          title: "My second Todo",
          completed: false
        },
        {
          id: 3,
          title: "My third Todo",
          completed: false
        }
      ]
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
