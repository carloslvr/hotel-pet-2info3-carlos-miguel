<script setup>
import { onMounted, ref } from 'vue';
import { RouterLink, useRoute } from 'vue-router';

const route = useRoute();
const API_URL = 'http://localhost:3000';

const tutor = ref({});
const naoEncontrado = ref(false);

async function carregarTutor() {
  try {
    const resposta = await fetch(`${API_URL}/tutores/${route.params.id}`);
    if (!resposta.ok) {
      naoEncontrado.value = true;
      return;
    }
    tutor.value = await resposta.json();
  } catch (erro) {
    console.error('Erro ao carregar os dados do tutor:', erro);
  }
}

onMounted(carregarTutor);
</script>

<template>
  <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Detalhes do Tutor</h1>
    </header>

    <p v-if="naoEncontrado">Opa, tutor não encontrado!</p>

    <div v-else>
      <p><strong>ID:</strong> {{ tutor.id }}</p>
      <p><strong>Nome:</strong> {{ tutor.nome }}</p>
      <p><strong>Telefone:</strong> {{ tutor.telefone }}</p>
    </div>

    <RouterLink
      class="btn btn-secondary"
      to="/tutores"
    >
      Voltar para a lista
    </RouterLink>
  </div>
</template>