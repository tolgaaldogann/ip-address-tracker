<template>
  <AddressTrackerPage msg="Welcome to Your Vue.js App"/>
</template>

<script>
import AddressTrackerPage from '../src/components/AddressTrackerPage.vue'

export default {
  name: 'App',
  components: {
    AddressTrackerPage
  }
}
</script>

<style>
#app {
  width: 100%;
  min-height: 100vh;
}

* {
  box-sizing: border-box;
}

html {
  font-family: "Roboto", sans-serif;
}

body {
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
