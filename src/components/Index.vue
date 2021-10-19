<template>
  <div id="container">
    <span>{{ hello }}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "@vue/runtime-core";

export default defineComponent({
  setup () {
    const hello = ref<string>('Hello Vue3')
    
    return {
      hello
    }
  }
})
</script>

<style lang="scss" scoped>
#container {
  width: 90%;
  height: 90%;
  max-width: 500px;
  max-height: 750px;
  span {
    font-size: 24px;
    color: #2189c5;
  }
}
</style>