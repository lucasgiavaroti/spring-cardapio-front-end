<script setup>
import { ref } from "vue";
import Cadastrar from "./components/Cadastrar.vue";
import Cards from "./components/Cards.vue";

var showCadastrar = ref(false);

const toggleCadastrar = () => {
  showCadastrar.value = !showCadastrar.value;
};

const closeCadastrar = () => {
  showCadastrar.value = false;
};
</script>

<template>
  <div
    style="
      background-color: #ffff;
      border-radius: 10px;
      padding: 2rem 0;
      min-height: 90vh;
    "
  >
    <h1 style="text-align: center">Cardápio</h1>
    <button @click="toggleCadastrar()">Cadastrar nova comida</button>
    <div class="container">
      <Cards />
      <Cadastrar v-if="showCadastrar" @close="closeCadastrar" />
    </div>
  </div>
</template>

<style scoped>
.container {
  padding: 0 0 1rem 0;
}
button {
  font-size: medium;
  margin: 2rem auto;
  display: block;
  padding: 0.5rem 1rem;
  background-color: rgba(255, 106, 0, 0.781);
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}
button:hover {
  background-color: rgb(226, 94, 0);
}
</style>
