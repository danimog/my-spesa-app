<script setup>
import { ref } from 'vue';
import { Client, Databases } from 'appwrite';

const spese = ref([]);

// Initialize the Appwrite client
const client = new Client()
  .setEndpoint('https://cloud.appwrite.io/v1') // Your Appwrite Endpoint
  .setProject('67850cca002d9b668487'); // Your project ID

const databases = new Databases(client);

const promise = databases.listDocuments(
  "67850fdd002ef99086c9",
  "67850fe70035f5c7bdb0",
  []
);

promise.then(function (response) {
  console.log(response);
  spese.value = response;
}, function (error) {
  console.log(error);
});

</script>

<template>
  <div class="container mx-auto mt-5">
    <h1 className="text-4xl font-bold my-5">
      Spesa App!
    </h1>

    <!-- {{ spese }} -->
    <p v-for="spesa in spese.documents" :key="spesa.$id">
      {{ spesa.prodotto }} - {{ spesa.quantita }} - {{ spesa.comprato }} - {{ spesa.note }}
    </p>

    <div class="w-full max-w-96">
      <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
            Username
          </label>
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            id="username" type="text" placeholder="Username">
        </div>
        <div class="mb-6">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
            Password
          </label>
          <input
            class="shadow appearance-none border border-red-500 rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
            id="password" type="password" placeholder="******************">
          <p class="text-red-500 text-xs italic">Please choose a password.</p>
        </div>
        <div class="flex items-center justify-between">
          <button
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            type="button">
            Sign In
          </button>
          <a class="inline-block align-baseline font-bold text-sm text-blue-500 hover:text-blue-800" href="#">
            Forgot Password?
          </a>
        </div>
      </form>
    </div>


  </div>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
