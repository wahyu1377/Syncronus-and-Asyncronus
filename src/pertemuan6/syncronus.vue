<script setup>
import { ref } from 'vue';


const birthYear = ref(2000); 
const age = ref(0); 

// synchronous untuk menghitung umur
function calculateAge() {
    console.log(" Menghitung umur...");
    let currentYear = new Date().getFullYear();
    age.value = currentYear - birthYear.value;
    console.log(" Umur berhasil dihitung:", age.value);
}
</script>

<template>
  <div class="p-4 max-w-md mx-auto bg-white shadow-lg rounded-lg">
    <h2 class="text-lg font-semibold mb-4">Hitung Umur</h2>

    <label class="block text-gray-700">Masukkan Tahun Lahir:</label>
    <input v-model="birthYear" type="number" class="w-full p-2 border rounded-md" @input="calculateAge" />

    <div class="mt-4 p-4 bg-blue-100 rounded-md">
      <p><strong>Umur Anda:</strong> {{ age }} tahun</p>
    </div>
  </div>
</template>
