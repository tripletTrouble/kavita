<script setup>
const props = defineProps({
    isOpen: {
        type: Boolean
    },
    playMedia: {
      type: Function,
      required: true
    },
    penerima: {
      type: String,
      required: true
    }
})
</script>

<template>
    <section
      id="opening"
      class="max-w-xl mx-auto h-screen bg-white relative overflow-hidden items-center justify-center transition-all duration-[3000]"
      :class="[!isOpen ? 'flex opacity-100' : 'opacity-0 hidden']"
    >
      <img
        src="./../assets/blue-flower.webp"
        alt="Blue Flower"
        class="absolute left-0 -bottom-[20%] sm:-bottom-[15%] opacity-70"
      />
      <div class="z-10 h-[70%]">
        <p class="text-xl text-center font-arabic">
          بِسْمِ ٱللَّٰهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ
        </p>
        <h1 class="text-[40px] mt-10 text-center font-cursive">
          Kavita & Deri
        </h1>
        <p class="text-center text-xl mt-2">Wedding Invitation</p>
        <div class="mt-7 flex items-center flex-col">
          <p class="text-center mb-3">Kepada Bapak/Ibu/Saudara/i</p>
          <p class="font-bold text-lg text-center mb-7">{{ penerima }}</p>
          <p class="text-center w-[75%]">
            Tanpa mengurangi rasa hormat, kami mengundang Bapak/Ibu/Saudara/i
            untuk menghadiri acara pernikahan kami.
          </p>
          <button type="button" @click="playMedia" class="bg-sky-600/80 text-white font-bold p-3 rounded-md mt-7">Buka Undangan</button>
        </div>
      </div>
    </section>
</template>