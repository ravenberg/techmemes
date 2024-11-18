<script setup>
import { onMounted, ref } from "vue";

const props = defineProps({
  name: String,
})

const alt = props.name.split('-')
  .map(word => word.charAt(0).toUpperCase() + word.slice(1))
  .join(' ');
const memeRef = ref(null)
const copied = ref(false)
const clipboardItem = ref(null)

const convertImageToClipboardItem = () => {
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
      clipboardItem.value = new ClipboardItem({ "image/png": blob })
    })
  }
}

const copyImage = () => {
  navigator.clipboard.write([clipboardItem.value])
  copied.value = true
  setTimeout(() => {
    copied.value = false
  }, 3000)
}

onMounted(() => {
  // The image need to be converted beforehand so it can write to clipboard within the click handler stack.
  convertImageToClipboardItem()
})
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