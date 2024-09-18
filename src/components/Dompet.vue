<script setup>
import {onBeforeUnmount, onMounted, ref} from 'vue';
import ClipboardJS from 'clipboard';

const copyBtn = ref(null);

onMounted(() => {
    const cb = new ClipboardJS(copyBtn.value)

    cb.on('success', () => {
        alert('Nomor rekening berhasil disalin!')
    })

    onBeforeUnmount(() => {
        cb.destroy();
    })
})
</script>

<template>
    <div class="flex flex-col items-center w-full py-16 bg-gradient-to-br from-sky-200 to-blue-300">
        <h1 class="text-center font-cursive text-3xl mb-7">Dompet Digital</h1>
        
        <div class="bg-slate-100 w-[80%] lg:w-[70%] p-5 rounded-xl flex flex-col items-center justify-center">
            <img src="./../assets/bsi.png" alt="Logo BSI" class="w-36">
            <hr class="border border-black w-[90%] mt-5">
            <div class="flex gap-4 items-end mb-3">
                <span class="mt-3 text-lg" id="norek">9744904730</span>
                <button ref="copyBtn" class="p-1 rounded-lg text-sm text-white bg-blue-700" data-clipboard-target="#norek">Copy</button>
            </div>
            <span class="font-bold">A.N. Kavita Febriani Putri</span>
        </div>
    </div>
</template>