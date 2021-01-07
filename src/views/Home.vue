<template>
  <div class="home">
    <HelloWorld  :keys="keys" :root="root"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  props: {
    root: Object,
    keys: Array
  }
}
</script>
