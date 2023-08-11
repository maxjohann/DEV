<script setup>
import { ref } from 'vue';
import MButton from '@/components/MButton.vue';
import router from '@/router';
import MeuCarrinho from '@/components/MeuCarrinho.vue';
import {carrinho, atualizaQuantidadeItem, removerItemCarrinho, deleteItens} from '@/_data/carrinho.js'
import MMessage from'@/components/MMessage.vue';
const nome = ref('')
const email = ref('')
const telefone = ref('')
const formaDePagamento = ref('')
const cpf = ref('')
const endereço = ref('')
const user = ref({
  avatar: null
})
function handleFileUpload(e) {
  const target = e.target
  if (target && target.files) {
    const file = target.files[0]
    user.value.avatar = URL.createObjectURL(file)
  }
}
function validar() {
  if (ok.value) {
    return false
  }
  if (senha.value === confirmacao.value) {
    return true;
  }
  else {
    return false;
  }
}
function formatarPreco(preco) {
  return 'R$ ' + preco.toFixed(2).replace('.', ',')
}
function Fim(){
  alert = "Compra Finalizada"
}

const confirmar = ref(false)
</script>

<template>
  <div class="carrinho">
    <h2>Meu carrinho</h2>
    <div class="wrap-carrinho">
      <m-messagge v-if="carrinho.itens.length === 0"/>
      <div v-else>
        <div class="item-carrinho" v-for="(item, index) in carrinho.itens" :key="index">
          <div class="info-livro">
            <div class="imagem-livro">
              <img :src="item.img" class="icon-capa-livro" />
            </div>
            <div class="detalhes-livro">
              <div>
                <p>{{ item.title }}</p>
                <p class="info-livro-preco">{{ formatarPreco(item.price) }}/un</p>
              </div>
              <div>
                <p>
                  Quantidade:
                  <input
                    type="number"
                    v-model="item.quantidade"
                    @change="atualizaQuantidadeItem(item)"
                    min="1"
                  />
                </p>
                <button @click="removerItemCarrinho(item)">&#128465;</button>
                <p>Total: {{ formatarPreco(item.total) }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
  <form class="info" @submit.prevent="aceitar = !aceitar">
    <p>Nome:</p>
    <input type="text" v-model="nome" minlength="3" maxlength="20" placeholder="Nome" required autocomplete="on" />
    <p>Email:</p>
    <input type="email" v-model="email" placeholder="Email" required autocomplete="on" />
    <p>telefone:</p>
    <input type="text" v-model="telefone" minlength="8" maxlength="15" required autocomplete="on">
    <p>forma de pagamento:</p>
    <input type="string" v-model="formaDePagamento">
    <m-button texto="Voltar" @click="$router.push({ name: 'livraria' })" />
    <div>
      <button class="botao" type="submit" @click="Fim">Finalizar</button>

    </div>
  </form>
</template>

<style scoped>
.wrap-carrinho .carrinho-total {
  position: fixed;
  bottom: 3%;
  font-size: 1.5rem;
  font-weight: bold;
}

.item-carrinho .info-livro {
  display: flex;
  justify-content: center;
  margin-bottom: 10px;
}
.detalhes-livro {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.detalhes-livro p {
  margin: 0;
}
.detalhes-livro div {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.detalhes-livro input[type='number'] {
  width: 50px;
  text-align: center;
  border: none;
  border-bottom: 1px solid black;
  background-color: transparent;
  margin-left: 10px;
}

.detalhes-livro button {
  background-color: transparent;
  border: none;
  cursor: pointer;
  font-size: 1.5rem;
  color: black;
  padding: 0;
  margin: 0;
}

.info-livro-preco {
  margin-left: auto;
}
.icon-capa-livro {
  width: 30px;
  margin-right: 10px;
}

</style>