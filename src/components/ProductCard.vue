<script setup>
defineProps({
  nome: String,
  preco: Number,
  imagem: String
})

const emit = defineEmits(['adicionar-carrinho'])
</script>

<template>
  <div class="card">
    <img :src="imagem" :alt="nome" class="card-img" />
    <div class="card-body">
      <h3>{{ nome }}</h3>
      <p class="preco">R$ {{ preco.toFixed(2) }}</p>
      <button @click="emit('adicionar-carrinho')" class="btn">Adicionar ao Carrinho</button>
    </div>
  </div>
</template>

<style scoped>
.card {
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  overflow: hidden;
  background-color: #ffffff;
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100%;
  box-sizing: border-box;
}
.card-img {
  width: 100%;
  height: 150px;
  object-fit: contain; 
  background-color: #f7fafc; 
  border-radius: 4px;
}
.card-body {
  text-align: center;
  margin-top: 0.8rem;
  width: 100%;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  justify-content: space-between;
}
.card-body h3 {
  color: #2d3748; 
  font-size: 1rem;
  margin: 0.5rem 0;
}
.preco {
  color: #2b6cb0;
  font-weight: bold;
  margin: 0.5rem 0;
}
.btn {
  background-color: #319795;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
  font-weight: bold;
  margin-top: auto;
}
.btn:hover {
  background-color: #2c7a7b;
}
</style>