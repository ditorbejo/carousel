<script setup>
import { onMounted, ref } from 'vue'

let direction = ref('right')

const imageSources = [
  {
    srcImage: 'https://picsum.photos/600/401',
    alt: 'image1'
  },
  {
    srcImage: 'https://picsum.photos/600/402',
    alt: 'image2'
  },
  {
    srcImage: 'https://picsum.photos/600/403',
    alt: 'image3'
  },
  {
    srcImage: 'https://picsum.photos/600/404',
    alt: 'image1'
  },
  {
    srcImage: 'https://picsum.photos/600/405',
    alt: 'image2'
  },
  {
    srcImage: 'https://picsum.photos/600/406',
    alt: 'image3'
  }
]

let counter = ref(0)
function slideLeft() {
  if (counter.value === 0) {
    return
  }
  counter.value = counter.value - 1
}
function slideRight() {
  if (counter.value === imageSources.length - 1) {
    return
  }
  counter.value = counter.value + 1
}
function changeSelectedItem(index) {
  console.log(index)
  counter.value = index
}
onMounted(() => {
  setInterval(() => {
    if (direction.value === 'right') {
      slideRight()
    } else if (direction.value === 'left') {
      slideLeft()
    }

    if (counter.value === 0) {
      direction.value = 'right'
    } else if (counter.value === imageSources.length - 1) {
      direction.value = 'left'
    }
  }, 5000)
})
</script>

<template>
  <div class="flex flex-row w-full h-full py-5 border-black border-2 items-center gap-1">
    <button class="p-3 border rounded-full" @click="slideLeft">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M10.5 19.5 3 12m0 0 7.5-7.5M3 12h18"
        />
      </svg>
    </button>
    <div class="border-black border-2 w-full px-6 overflow-hidden">
      <div class="image-wrapper flex flex-row gap-2 items-center h-[300px] relative">
        <img
          :src="item.srcImage"
          :alt="item.alt"
          v-for="(item, index) in imageSources"
          :key="item.alt"
          :style="`transform: translateX(-${counter * 100}%); left: ${index * 100}%`"
          class="h-full object-cover w-full -translate-x-[100%] absolute px-2 transition-transform duration-500 ease-in"
        />
      </div>
    </div>
    <button class="p-3 border rounded-full" @click="slideRight">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="1.5"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M13.5 4.5 21 12m0 0-7.5 7.5M21 12H3"
        />
      </svg>
    </button>
  </div>
  <div class="border-black border-b-2 border-l-2 border-r-2 w-full px-10 py-10 flex items-center">
    <div class="border-black border-2 w-full h-full grid grid-cols-5 gap-1 px-1 py-1">
      <img
        :src="item.srcImage"
        :alt="item.alt"
        v-for="(item, index) in imageSources"
        :key="item.alt"
        class="h-full object-cover w-full"
        @click="changeSelectedItem(index)"
      />
    </div>
  </div>
</template>
