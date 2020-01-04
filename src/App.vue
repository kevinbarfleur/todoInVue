<template>
  <Todos />
</template>

<script>
import Todos from './components/Todos'

export default {
  name: 'app',
  components: {
    Todos
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  font-family: 'Avenir', Helvetica, sans-serif;
}

body {
  color: #212121;
}
</style>