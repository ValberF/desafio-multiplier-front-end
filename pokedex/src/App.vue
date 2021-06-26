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

::-webkit-scrollbar {
  width: 1rem;
}
 
::-webkit-scrollbar-thumb {
  background: #a1a1a1; 
  border-radius: 15px;
}

::-webkit-scrollbar-thumb:hover {
  background: #717171; 
}

input {
  margin-bottom: 25px !important;
}
</style>
