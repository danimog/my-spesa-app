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
  <div>
    {{ spese }}

    <p v-for="spesa in spese.documents" :key="spesa.$id">
      {{ spesa.prodotto }} - {{ spesa.quantita }} - {{ spesa.comprato }} - {{ spesa.note }}
    </p>

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
