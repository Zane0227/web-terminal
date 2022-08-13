<template>
  <div id="app">
    <XTerm socketURI="ws://localhost:4001"/>
  </div>
</template>

<script>
import XTerm from './components/XTerm'

export default {
  name: 'App',
  components: {
    XTerm
  },
}
</script>

<style>
body {
  margin: 0
}
</style>
