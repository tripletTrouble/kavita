<script setup>
import Opening from './components/Opening.vue';
import Couple from './components/Couple.vue';
import {ref} from 'vue';

const isOpen = ref(false);
</script>

<template>
  <div class="w-screen min-h-screen bg-black">
    <Opening @open="isOpen=true" :isOpen="isOpen"></Opening>
    <section id="content" :class="[isOpen ? 'flex' : 'hidden']" class="max-w-xl mx-auto h-screen bg-white items-center justify-center transition-all duration-[3000]">
      <Couple/>
    </section>
  </div>
</template>
