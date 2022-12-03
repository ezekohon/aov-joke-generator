<template>
  <div class="w-full h-full flex justify-center items-center flex-col" v-if="!loading">
    <span class="text-3xl mb-5">{{ setup }}</span>
    <button class="rounded-lg shadow w-24 h-12 bg-gray-200" @click="handleReveal" v-if="!showReveal">Tell Me!</button>
    <span class="text-2xl text-gray-400 mb-10" v-if="showReveal">{{ delivery }}</span>
    <button class="rounded-lg shadow w-24 h-12 bg-gray-200" @click="handleAnother" v-if="showAnother">Another</button>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const loading = ref(true)
const setup = ref('')
const delivery = ref('')
const showReveal = ref(false)
const showAnother = ref(false)

onMounted(async () => {
  loadJoke()
})

const loadJoke = async () => {
  loading.value = true
  const joke = await fetch('https://v2.jokeapi.dev/joke/christmas').then((r) => r.json())
  setup.value = joke.setup
  delivery.value = joke.delivery
  loading.value = false
}

const handleReveal = () => {
  showReveal.value = true
  showAnother.value = true
}

const handleAnother = () => {
  showAnother.value = false
  showReveal.value = false
  loadJoke()
}
</script>
