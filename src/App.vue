<template lang="pug">
router-view
</template>

<script lang="ts">
import { defineComponent } from 'vue'
// import * as io from 'socket.io-client'
// import Hosts from '@/api/hosts'
// import { useRouter } from 'vue-router'
export default defineComponent({
  name: 'App',
  setup: () => {
    // const router = useRouter()
    return {
    }
  }
})
</script>

<style>
html,
body {
  overflow-y: hidden;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100%;
  /* text-align: center; */
  /* color: #2c3e50; */
}

#app .clear-all-notification-btn {
  position: fixed;
  top: 24px;
  right: 24px;
  z-index: 3000;
}
</style>
