<script setup>
import { ref, reactive } from "vue";
import axios from "axios";

const comments = ref(null);
const formData = reactive({
  name: null,
  body: null,
});
const fmt = new Intl.DateTimeFormat("id-ID", {
  day: "numeric",
  month: "long",
  year: "numeric",
  timeZone: "Asia/Jakarta",
});

function parseDate(date) {
  return fmt.format(new Date(date));
}

async function fetchComment() {
  await axios
    .get("http://192.168.1.28:8000/api/comments")
    .then((res) => (comments.value = res.data))
    .catch((err) => {
      alert(err.response.data.message);
    });
}

async function send() {
  await axios
    .post("http://192.168.1.28:8000/api/comments", formData)
    .then((res) => {
      fetchComment();
      formData.name = null;
      formData.body = null;
    });
}

fetchComment();
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-pink-200 pt-16 pb-16 to-gray-100 w-full flex flex-col items-center"
    id="wishes"
  >
    <h2 class="text-center font-cursive text-2xl">Ucapan Kepada Mempelai</h2>
    <div class="border rounded-lg mt-7 p-4 w-[90%] lg:w-[70%] border-black">
      <div class="mb-2">
        <label for="UserEmail" class="block text-sm font-medium text-gray-700">
          Nama
        </label>
        <input
          type="email"
          id="UserEmail"
          placeholder="Abdullah"
          class="mt-1 w-full rounded-md border-gray-200 bg-slate-50 bg-opacity-40 shadow-sm sm:text-sm"
          v-model="formData.name"
        />
      </div>
      <div class="mb-2">
        <label for="UserEmail" class="block text-sm font-medium text-gray-700">
          Ucapan
        </label>
        <textarea
          type="email"
          id="UserEmail"
          placeholder="Selamat menempuh hidup baru"
          rows="3"
          class="mt-1 w-full rounded-md border-gray-200 bg-slate-50 bg-opacity-40 shadow-sm sm:text-sm"
          v-model="formData.body"
        ></textarea>
      </div>
      <div class="flex justify-end">
        <button
          type="button"
          @click="send"
          class="bg-sky-500 text-white text-sm p-3 rounded-lg"
        >
          Kirim Ucapan
        </button>
      </div>
    </div>
    <div
      class="h-80 w-[90%] lg:w-[70%] border border-black rounded-lg flex flex-col gap-3 mt-7 p-5"
    >
      <h3 class="font-bold text-center">Ucapan-Ucapan</h3>
      <div class="flex flex-col gap-3 overflow-y-auto">
        <div
          v-for="item in comments"
          class="bg-sky-200 bg-opacity-50 p-4 rounded-lg"
        >
          <div class="flex justify-between">
            <span class="text-sm font-bold">{{ item["name"] }}</span>
            <span class="text-xs"> {{ parseDate(item["created_at"]) }}</span>
          </div>
          <p class="text-xs mt-2">{{ item["body"] }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
