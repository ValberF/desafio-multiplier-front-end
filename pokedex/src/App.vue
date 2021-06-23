<template>
  <div id="app">
    <Header />
    <Content />
  </div>
</template>

<script>
import Content from './components/templates/Content.vue'
import Header from './components/templates/Header.vue'

export default {
  components: {
    Header,
    Content
  }
}
</script>

<style>
#app{
  background-color: #D4F7FA;
  min-height: 100vh;
}
</style>
