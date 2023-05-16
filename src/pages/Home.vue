<template lang="pug">
iframe(:src="'http://192.168.0.57:3001'")
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, nextTick } from "vue";

export default defineComponent({
  name: "Home",
  // components: { live2d },
  setup: () => {
    return {  };
  },
});
</script>

<style scoped>
iframe {
  position: fixed;
  height: 100vh;
  width: 100vw;
  left: 0;
  top: 0;
  border: none;
}
</style>
