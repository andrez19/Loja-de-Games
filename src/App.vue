<script setup>
import { ref, computed } from 'vue'
import ProductCard from './components/ProductCard.vue'

// 1. Reatividade: Contador de itens no carrinho
const itensNoCarrinho = ref(0)

// 2. Campo de busca (v-model)
const termoBusca = ref('')

// Lista de produtos
const produtos = ref([
  { id: 1, nome: 'GTA 6 p/ Playstation 5', preco: 349.00, imagem: './img/gta-6.jpg' },
  { id: 2, nome: 'Resident Evil Requiem p/ Xbox Series X/S', preco: 249.00, imagem: './img/resident.jpg' },
  { id: 3, nome: 'Zelda Ocarina of Time Remake p/ Nintendo Switch 2', preco: 399.00, imagem: './img/zelda.jpg' },
  { id: 4, nome: 'Expedition 33 para PC', preco: 199.90, imagem: './img/expedition33.jpg' }
])

// Incrementa o carrinho
function adicionarAoCarrinho() {
  itensNoCarrinho.value++
}

// 3. Computed Property para filtrar os produtos em tempo real
const produtosFiltrados = computed(() => {
  return produtos.value.filter(produto =>
    produto.nome.toLowerCase().includes(termoBusca.value.toLowerCase())
  )
})
</script>

<template>
  <div class="container">
    <header class="header">
      <h1>Loja de Games</h1>
      <div class="carrinho">
        Itens no carrinho: <strong>{{ itensNoCarrinho }}</strong>
      </div>
    </header>

    <!-- Campo de Busca -->
    <div class="busca-box">
      <input
        v-model="termoBusca"
        type="text"
        placeholder="Buscar produto por nome..."
        class="input-busca"
      />
    </div>

    <!-- Listagem de Cards -->
    <div v-if="produtosFiltrados.length > 0" class="grid-produtos">
      <ProductCard
        v-for="produto in produtosFiltrados"
        :key="produto.id"
        :nome="produto.nome"
        :preco="produto.preco"
        :imagem="produto.imagem"
        @adicionar-carrinho="adicionarAoCarrinho"
      />
    </div>
    <p v-else class="vazio">Nenhum produto encontrado.</p>
  </div>
</template>

<style>
body {
  font-family: Arial, sans-serif;
  background: linear-gradient(to left, rgb(47, 0, 255),cyan);
  width: 100%;
  min-height: 100vh;
  margin: 0;
  color: white;
}

h1 {
  font-size: 3em;
  margin: 0;
}
.container {
  max-width: 800px;
  margin: 2rem auto;
  padding: 0 1rem;
}
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 1rem;
  margin-bottom: 1.5rem;
  font-style: italic;
  text-decoration: underline;
}
.carrinho {
  background-color: white;
  color: darkred;
  padding: 20px;
  border-radius: 20px;
  border: 3px solid darkred;
}
.busca-box {
  margin-bottom: 1.5rem;
}
.input-busca {
  width: 100%;
  padding: 0.75rem;
  font-size: 1rem;
  border: 1px solid #cbd5e0;
  border-radius: 6px;
  box-sizing: border-box;
}
.grid-produtos {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 1.2rem;
}
.vazio {
  text-align: center;
  color: #a0aec0;
  margin-top: 2rem;
}

</style>