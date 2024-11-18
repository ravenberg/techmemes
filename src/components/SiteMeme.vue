<script setup>
import { ref } from "vue";

const props = defineProps({
  name: String,
})

const alt = props.name.replace(/-([a-z])/g, (g) => g[1].toUpperCase())
const memeRef = ref(null)
const copied = ref(false)

// copy image to clipboard using the clipboard API
const copyImage = () => {
  const img = memeRef.value
  const canvas = document.createElement("canvas")
  const ctx = canvas.getContext("2d")
  const imgElement = new Image()
  imgElement.src = img.src
  imgElement.onload = () => {
    canvas.width = imgElement.width
    canvas.height = imgElement.height
    ctx.drawImage(imgElement, 0, 0)
    canvas.toBlob((blob) => {
      const item = new ClipboardItem({ "image/png": blob })
      navigator.clipboard.write([item])
    })
  }

  copied.value = true
  setTimeout(() => {
    copied.value = false
  }, 3000)
}
</script>

<template>
  <li class="px-4 relative">
    <button class="absolute right-7 bottom-2 rounded py-2 px-1 bg-gray-800 text-gray-200 opacity-70 hover:opacity-100 transition" @click="copyImage">
      <span v-if="copied">✅ Copied</span>
      <span v-else>📋 Copy</span>
    </button>
    <img ref="memeRef" class="rounded-3xl" :src="`/memes/${name}.webp`" :alt="alt">
  </li>
</template>

<style scoped>

</style>