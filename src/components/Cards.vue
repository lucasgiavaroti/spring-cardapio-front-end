<template>
  <div class="cards-container">
    <div
      class="card"
      v-if="foods.length > 0"
      v-for="(foodItem, index) in foods"
      :key="index"
    >
      <h3 class="title" style="margin: 0">{{ foodItem.title }}</h3>
      <figure>
        <img class="image" :src="foodItem.image" alt="Imagem da comida" />
      </figure>
      <h4 class="price">R$ {{ foodItem.price }}</h4>
      <div class="delete">
        <button @click="deleteFood(foodItem.id)">Deletar</button>
      </div>
    </div>
    <div v-else>
      <h3 style="text-transform: none">
        Não existem pratos cadastrados no momento!
      </h3>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  name: "CardList",
  setup() {
    const foods = ref([]); //Array que armazena todos os cards

    const deleteFood = async (id) => {
      try {
        await fetch(`http://localhost:8080/food/${id}`, {
          method: "DELETE",
        });
        foods.value = foods.value.filter((food) => food.id !== id); // Filtra o array deletando o item
      } catch (error) {
        console.error("Erro ao deletar item:", error);
      }
    };

    const fetchFoods = async () => {
      try {
        const response = await fetch("http://localhost:8080/food");
        const data = await response.json();
        foods.value = data; // Armazena todos os itens retornados
      } catch (error) {
        console.error("Erro ao buscar dados:", error);
      }
    };
    onMounted(fetchFoods);

    return { foods, deleteFood };
  },
};
</script>

<style scoped>
.cards-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 5rem;
}
.card {
  margin-top: 3rem;
  background-color: #ffcc6e41;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 500px;
  width: 350px;
  border-radius: 10px;
  box-shadow: 2.6px 2.8px 2.2px rgba(0, 0, 0, 0.037),
    6.3px 6.7px 5.3px rgba(0, 0, 0, 0.053),
    11.8px 12.5px 10px rgba(0, 0, 0, 0.065),
    21px 22.3px 17.9px rgba(0, 0, 0, 0.077),
    39.3px 41.8px 33.4px rgba(0, 0, 0, 0.093),
    94px 100px 80px rgba(0, 0, 0, 0.13);
  cursor: pointer;
}
.card:hover {
  transform: scale(1.05);
  transition: all 0.3s;
}
h3 {
  text-transform: capitalize;
  color: rgba(24, 24, 24, 0.664);
  font-size: 1.5rem;
}
p {
  font-size: 1rem;
  color: rgba(24, 24, 24, 0.664);
  font-weight: 500;
  margin-top: 10px;
}
img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 10px;
}
h4 {
  background-color: rgba(247, 170, 115, 0.651);
  padding: 0.2rem 0.7rem;
  border-radius: 7px;
  color: rgba(24, 24, 24, 0.664);
}
.delete button {
  background-color: #ff000070;
  color: white;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 5px;
  margin-top: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}
.delete button:hover {
  background-color: #ff0000ce;
}
</style>
