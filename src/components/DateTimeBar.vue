<script setup>
import { ref, computed } from 'vue'
import { format } from 'date-fns'

const now = ref(new Date())

const date = computed(() => {
    return format(now.value, 'EEEE, LLLL d, yyyy')
})

const time = computed(() => {
    return format(now.value, 'hh:mm:ss aaa')
})

setInterval(() => {
  now.value = new Date()
}, 1000)

</script>

<template>
 <div>
   <p> {{ date }} </p>
   <p> {{ time }} </p>
 </div>
</template>

<style scoped>
    div {
      display: flex;
      justify-content: space-between;
    }
</style>
