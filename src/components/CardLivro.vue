<script setup>
import {adicionarAoCarrinho} from '@/_data/carrinho.js'
import MButton from "@/components/MButton.vue";

const props = defineProps({
    livro: Object
})

function formatarPreco(preco) {
  return 'R$ ' + preco.toFixed(2).replace('.', ',')
}
</script>

<template>
         <div class="card-livro" >
        <div class="card-info-livro">
          <div class="wrap-livro">
            <img :src="props.livro.img" alt="Capa do livro" class="capa-livro" />
          </div>
          <p class="titulo-livro">{{ props.livro.title }}</p>
          <p class="autor-livro">{{ props.livro.author }}</p>
          <p class="preco-livro">{{ formatarPreco(props.livro.price) }}</p>
        </div>
        <div class="card-buttons-livros">
          <MButton @click="adicionarAoCarrinho(props.livro)" texto="Adicionar Carrinho"/>
        </div>
      </div>     
</template>

<style scoped>

.card-livro {
  margin: 5px 10px;
  padding: 10px;
  background-color: rgb(31, 29, 27);
  border-radius: 10px;
  width: 180px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.wrap-livro {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  border-radius: 10px;
  width: 180px;
  height: 270px;
}
.capa-livro {
  width: 90%;
  max-height: 100%;
}

.card-livro p {
  margin: 0;
}

.card-livro .titulo-livro {
  font-weight: bold;
  margin-bottom: 5px;
}
.addCarrinho{
  background-color: rgb(68, 57, 57);
    color: wheat;
    font-size: 1.1rem;
    border: 1px solid wheat;
    border-radius: 5px;
    padding: 5px 10px;
    cursor: pointer;
}
</style>