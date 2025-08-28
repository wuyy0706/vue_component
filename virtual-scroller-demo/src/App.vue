<template>
  <div id="app">
    <VirtualScrollerDemo />
  </div>
</template>

<script>
import VirtualScrollerDemo from './components/VirtualScrollerDemo.vue'

export default {
  name: 'App',
  components: {
    VirtualScrollerDemo
  }
}
</script>

<style>
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: #f5f7fa;
  margin: 0;
  padding: 20px;
}

#app {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 100vh;
}
</style>
