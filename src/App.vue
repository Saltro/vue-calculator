<template>
  <index></index>
</template>

<script lang="ts">
import { defineComponent } from '@vue/runtime-core';
import Index from './components/Index.vue';

export default defineComponent({
  components: {
    Index,
  },
})
</script>

<style lang="scss">
@font-face {
  src: url('/PINGFANG\ SC\ REGULAR.TTF');
  font-family: 'PingFang';
}

* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-width: 100vw;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #EAEAEA;
  user-select: none;
  font-family: 'PingFang';
}
</style>
