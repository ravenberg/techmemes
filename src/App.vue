<script setup>
import SiteHeader from "./components/SiteHeader.vue";
import SiteFooter from "./components/SiteFooter.vue";
import SiteMeme from "./components/SiteMeme.vue";

// Add memes in /public/memes.
// List file name here without extension.
// It needs to be a webp file.
const memes = [
  "design-feedback",
];
</script>

<template>
  <main class="container mx-auto">
    <SiteHeader />
    <ul class="grid grid-cols-1 lg:grid-cols-2 2xl:grid-cols-3 gap-10">
      <SiteMeme v-for="meme in memes" :name="meme" />
    </ul>
    <SiteFooter />
  </main>
</template>

<style scoped>
</style>
