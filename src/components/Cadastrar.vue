<script setup>
import { ref } from "vue";

// Propriedades reativas para armazenar os dados do formulário
const title = ref("");
const price = ref("");
const image = ref("");

// Função para enviar os dados para a API
const submitForm = async (event) => {
  try {
    const response = await fetch("http://localhost:8080/food", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        title: title.value,
        price: parseFloat(price.value.replace(",", ".")),
        image: image.value,
      }),
    });
  } catch (error) {
    console.error("Error:", error.message);
  }
};
</script>

<template>
  <form @submit="submitForm">
    <h2 class="title">Cadastrar nova comida</h2>
    <label for="title">Nome:</label>
    <input type="text" id="title" v-model="title" required />

    <label for="price">Preço:</label>
    <input type="text" id="price" v-model="price" required />

    <label for="image">Imagem (URL):</label>
    <input type="text" id="image" v-model="image" required />

    <div class="buttons">
      <button type="submit">Cadastrar</button>
      <button type="button" @click="$emit('close')">Voltar</button>
    </div>
  </form>
</template>

<style scoped>
form {
  width: 50vw;
  height: 70vh;
  background-color: rgba(255, 255, 255, 0.911);
  border-radius: 10px;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border: 1px solid #ccc;
  box-shadow: 2.6px 2.8px 2.2px rgba(0, 0, 0, 0.037),
    6.3px 6.7px 5.3px rgba(0, 0, 0, 0.053),
    11.8px 12.5px 10px rgba(0, 0, 0, 0.065),
    21px 22.3px 17.9px rgba(0, 0, 0, 0.077),
    39.3px 41.8px 33.4px rgba(0, 0, 0, 0.093);
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
form input {
  margin: 1rem 0;
  padding: 0.5rem;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 50%;
}
.buttons {
  display: flex;
  justify-content: left;
  gap: 2rem;
}
form button {
  margin: 1rem 0;
  padding: 0.5rem;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  background-color: rgba(255, 106, 0, 0.781);
  color: rgba(24, 24, 24, 0.664);
  font-size: 0.9rem;
  font-weight: bold;
  transition: background-color 0.3s;
  width: 10rem;
}
</style>
