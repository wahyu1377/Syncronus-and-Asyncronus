<script setup>
import { ref } from 'vue';


const user = ref(null);
const loading = ref(false);
const errorMessage = ref("");

// Callback
function getUserData(callback) {
    loading.value = true;
    setTimeout(() => {
        let fetchedUser = { id: 1, name: "Wahyu", job: "Developer" };
        callback(null, fetchedUser);
    }, 2000);
}

// Promise
function processUserData(user) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (user) {
                user.status = "Aktif";
                resolve(user);
            } else {
                reject(" Data tidak ditemukan!");
            }
        }, 2000);
    });
}

// Async/Await
async function fetchUser() {
    try {
        errorMessage.value = "";
        getUserData(async (error, fetchedUser) => {
            if (error) {
                errorMessage.value = "Terjadi kesalahan saat mengambil data!";
            } else {
                user.value = await processUserData(fetchedUser);
            }
            loading.value = false;
        });
    } catch (err) {
        errorMessage.value = err;
        loading.value = false;
    }
}
</script>

<template>
  <div class="p-4 max-w-md mx-auto bg-white shadow-lg rounded-lg">
    <h2 class="text-lg font-semibold mb-4">Data Pengguna</h2>

    <button @click="fetchUser" class="bg-blue-500 text-white py-2 px-4 rounded-md hover:bg-blue-700">
      Ambil Data Pengguna
    </button>

    <div v-if="loading" class="mt-4 text-gray-500">⏳ Mengambil data...</div>
    <div v-if="errorMessage" class="mt-4 text-red-500">{{ errorMessage }}</div>

    <div v-if="user" class="mt-4 p-4 bg-green-100 rounded-md">
      <p><strong>Nama:</strong> {{ user.name }}</p>
      <p><strong>Pekerjaan:</strong> {{ user.job }}</p>
      <p><strong>Status:</strong> {{ user.status }}</p>
    </div>
  </div>
</template>
