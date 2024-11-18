<script setup>
const currentYear = new Date().getFullYear();
</script>

<template>
  <footer class="bg-gray-800 rounded-3xl mt-10 mb-4 mx-4 sm:mx-0">
    <div class="mx-auto max-w-7xl px-6 py-12 md:flex md:items-center md:justify-between lg:px-8">
      <p class="text-center text-sm/6 text-gray-400 md:order-1 md:mt-0">&copy; {{ currentYear }} <a href="https://x.com/akhibrown" class="underline">Lee Ravenberg</a>. All rights reserved.</p>
    </div>
  </footer>
</template>

<style scoped>

</style>