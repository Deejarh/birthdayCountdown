<script setup>
import CountdownHeader from "@/components/CountdownHeader.vue";
import CountdownSegment from "@/components/CountdownSegment.vue";

import { onUnmounted, ref} from 'vue'

const days = ref(0)
const hours = ref(0)
const minutes = ref(0)
const seconds = ref(0)
const isBirthday = ref(false)

const interval = setInterval(() => { 
  const sec = 1000
  const min = sec * 60
  const hr = min * 60
  const day = hr * 24

  let today = new Date(),
      dd = String(today.getDate()),
      mm = String(today.getMonth()),
      yyyy = today.getFullYear(),
      nextYear = yyyy + 1,
      dayMonth = "09/21/",
      birthday = dayMonth + yyyy;
  
  today = mm + "/" + dd + "/" + yyyy;
  if (today > birthday) {
    birthday = dayMonth + nextYear;
  }
  const countdown = new Date (birthday).getTime()
    const now = new Date().getTime()

    
      const diff = countdown - now
     days.value = Math.floor(diff/day)
     hours.value =  Math.floor(diff % day /hr)    
     minutes.value = Math.floor(diff % hr / min)
     seconds.value = Math.floor(diff % min/ sec)

     if ( countdown < 0) {

    isBirthday = true 
    clearInterval(interval)
     }
  }, 1000) 
  onUnmounted(() => clearInterval(interval))

</script>
<template>
  <div class="app-wrapper">
    <div class="countdown-box" v-if="isBirthday">
    <p class=" text-lg font-medium" > Its My Birthday</p> 
    <p class=" flex  justify-center items-center"> 💃 🎂 🎉</p>

    </div>
    <div v-else class="countdown-box">
      <CountdownHeader />
      <main class="flex justify-center">
        <CountdownSegment data-test="days" label="days" :number=days />
        <CountdownSegment data-test="hours" label="hours" :number=hours />
        <CountdownSegment data-test="minutes" label="minutes" :number=minutes />
        <CountdownSegment data-test="seconds" label="seconds" :number=seconds />
      </main>
    </div>
  </div>
</template>

<style scoped>
.app-wrapper {
  @apply flex items-center justify-center w-full h-full p-10;
}
.countdown-box {
  @apply shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px];
}
body {
  @apply bg-gray-100;
}
</style>
