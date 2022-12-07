<script setup>
import { ref } from 'vue'

const setup = ref(null)
const delivery = ref(null)
const isDeliveryVisible = ref(false)


const showDelivery = () => isDeliveryVisible.value = true
const fetchJoke = async () => {
  isDeliveryVisible.value = false
  setup.value = null
  delivery.value = null
  try {
    const response = await (await fetch('https://v2.jokeapi.dev/joke/christmas')).json()
    setup.value = response.setup
    delivery.value = response.delivery
  } catch (error) {
    console.error(error)
    alert('Something went wrong!')
  }

}

fetchJoke()

</script>

<template>
  <div class="w-full h-full flex justify-center items-center">
    <div class="max-w-xs w-full flex flex-col">
      <div v-if="setup"  class="w-3/4 p-4 rounded-2xl bg-teal-800 text-white self-start">
        {{ setup }}
      </div>
      <div v-if="(delivery && isDeliveryVisible )"  class="w-3/4 mt-2 p-4 rounded-2xl bg-red-800 text-white self-end">
        {{ delivery }}
      </div>
      <button v-if="isDeliveryVisible" class="bg-green col-span-1 rounded-lg py-2 hover:opacity-90 w-full mx-auto mt-4" @click="fetchJoke">
       Another
      </button>
      <button v-else-if="setup" class="bg-green col-span-1 rounded-lg py-2 hover:opacity-90 w-full mx-auto mt-4" @click="showDelivery">
        Tell me!
      </button>
    </div>
  </div>
</template>


