<template>
  <Todos></Todos>
</template>

<script>
import Todos from "./components/Todos"

export default {
  name: "app",
  components: {
    Todos
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  font-family: "Avenir", Helvetica, sans-serif;
  color: #212121;
}

body {
  display: flex;
  // flex-direction: column;
  justify-content: center;
  align-content: center;
}
</style>