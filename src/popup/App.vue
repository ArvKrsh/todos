<template>
  <hello-world />
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'App',
  components: { HelloWorld }
}
</script>

<style>
html {
  width: 400px;
  height: 400px;
  margin: 10px;
  background-color: rgb(246, 251, 252);
}
* {
  padding: 0;
  margin: 0;
}
</style>
