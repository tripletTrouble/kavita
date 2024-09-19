<script setup>
import Opening from "./components/Opening.vue";
import Couple from "./components/Couple.vue";
import Acara from "./components/Acara.vue";
import Quotes from "./components/Quotes.vue";
import Wishes from "./components/Wishes.vue";
import { onMounted, ref } from "vue";
import Dompet from "./components/Dompet.vue";

const isOpen = ref(false);
const isPlaying = ref(false);
const audioPlayer = ref(null);
const penerima = ref("");
const playMedia = function () {
  isOpen.value = true;
  isPlaying.value = true;
  audioPlayer.value.play();
};
const toggleMedia = function () {
  if (isPlaying.value) {
    isPlaying.value = false;
    audioPlayer.value.pause();
  } else {
    isPlaying.value = true;
    audioPlayer.value.play();
  }
};

onMounted(() => {
  penerima.value = new URLSearchParams(window.location.search).get("to");
});
</script>

<template>
  <div
    class="bg-white bg-opacity-80 fixed bottom-2 left-[50%] -translate-x-[50%] z-30 py-4 px-5 rounded-lg"
    :class="[isOpen ? 'block' : 'hidden']"
  >
    <div class="relative flex text-sm gap-5">
      <a href="#couple" class="font-bold">Couple</a>
      <a href="#event" class="font-bold">Event</a>
      <a href="#wishes" class="font-bold">Wishes</a>
      <a href="#quotes" class="font-bold">Quotes</a>
      <button
        class="absolute -right-10 -top-10 bg-pink-400 p-1 rounded-lg text-sm z-30"
        @click="toggleMedia"
      >
        {{ isPlaying ? "Pause" : "Play" }}
      </button>
    </div>
  </div>
  <div class="w-screen min-h-screen bg-black">
    <audio src="sound.mp3" ref="audioPlayer" class="hidden invisible"></audio>
    <Opening
      @open="isOpen = true"
      :isOpen="isOpen"
      :playMedia="playMedia"
      :penerima="penerima"
    ></Opening>
    <section
      id="content"
      :class="[isOpen ? 'flex' : 'hidden']"
      class="max-w-xl mx-auto bg-white items-center flex flex-col justify-center transition-all duration-[3000]"
    >
      <Couple />
      <Acara />
      <Wishes />
      <Dompet />
      <Quotes />
    </section>
  </div>
</template>
