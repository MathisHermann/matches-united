<script setup>
import { ref } from 'vue'
import List from './List.vue'

defineProps({
  msg: String,
})
const count = ref(0)

</script>


<script>
export default {
  data() {
    return {
      rows: ['Hello Wordle!', 'Hello !']
    }
  }
}
</script>

<template>
<List :rows="rows"/>

<div>
  <label for="from" class="block text-sm font-medium text-gray-700">Von</label>
  <div class="mt-1">
    <input type="text" name="from" id="from" class="block w-full rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm" placeholder="you@example.com">
  </div>
</div>

    
  <h1>{{ msg }}</h1>

  <div class="bg-green-100 card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank">create-vue</a>, the official Vue + Vite
    starter
  </p>
  <p>
    Install
    <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
