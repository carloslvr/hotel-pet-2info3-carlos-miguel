<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const API_URL = 'http://localhost:3000';
const router = useRouter();

const estados = [
  'AC','AL','AP','AM','BA','CE','DF','ES','GO','MA','MT','MS','MG','PA',
  'PB','PR','PE','PI','RJ','RN','RS','RO','RR','SC','SP','SE','TO',
];

const novoTutor = ref({
  nome: '',
  cpf: '',
  telefone: '',
  email: '',
  nascimento: '',
  rua: '',
  numero: '',
  bairro: '',
  cidade: '',
  estado: '',
  cep: '',
});

async function salvarTutor() {
  await fetch(`${API_URL}/tutores`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(novoTutor.value),
  });
  router.push('/tutores');
}
</script>

<template>
  <div>
    <header class="mb-4">
      <h1 class="text-2xl font-bold">Cadastro de Tutores</h1>
      <p class="text-body-secondary mb-0">Cadastro de Tutores no sistema.</p>
    </header>

    <form @submit.prevent="salvarTutor">
      
      <div class="col-md-6">
        <label
          for="nome"
          class="form-label"
          >Nome do Tutor:</label
        >
        <input
          type="text"
          id="nome"
          v-model="novoTutor.nome"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6">
        <label
          for="telefone"
          class="form-label"
          >Telefone:</label
        >
        <input
          type="tel"
          id="telefone"
          v-model="novoTutor.telefone"
          class="form-control"
          required
        />
      </div>

       <div class="col-md-6">
        <label
          for="cpf"
          class="form-label"
          >Cpf/Cnpj:</label
        >
        <input
          type="text"
          id="cpf"
          v-model="novoTutor.cpf"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6">
        <label
          for="cpf"
          class="form-label"
          >E-mail:</label
        >
        <input
          type="email"
          id="email"
          v-model="novoTutor.email"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6">
        <label
          for="nascimento"
          class="form-label"
          >Data de Nascimento:</label
        >
        <input
          type="date"
          id="nascimento"
          v-model="novoTutor.nascimento"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6">
        <label
          for="rua"
          class="form-label"
          >Insira sua Rua:</label
        >
        <input
          type="text"
          id="rua"
          v-model="novoTutor.rua"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6">
        <label
          for="bairro"
          class="form-label"
          >Insira seu Bairro:</label
        >
        <input
          type="text"
          id="bairro"
          v-model="novoTutor.bairro"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6">
        <label
          for="cidade"
          class="form-label"
          >Insira sua Cidade:</label
        >
        <input
          type="text"
          id="cidade"
          v-model="novoTutor.cidade"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6">
        <label
          for="numero"
          class="form-label"
          >Insira o Número de sua casa:</label
        >
        <input
          type="text"
          id="numero"
          v-model="novoTutor.numero"
          class="form-control"
          required
        />
      </div>

      <div class="col-md-6">
        <label
          for="estado"
          class="form-label"
          >Insira seu Estado:</label
        >
         <select
    id="estado"
    v-model="novoTutor.estado"
    class="form-select"
    required
  >
    <option value="" disabled>Selecione</option>
    <option
      v-for="estado in estados"
      :key="estado"
      :value="estado"
    >
      {{ estado }}
    </option>
  </select>
      </div>

      <div class="col-md-6">
        <label
          for="cep"
          class="form-label"
          >Insira seu CEP:</label
        >
        <input
          type="text"
          id="cep"
          v-model="novoTutor.cep"
          class="form-control"
          required
        />
      </div>

      <button
        type="submit"
        class="btn btn-success mt-3"
      >
        Salvar Tutor
      </button>
    </form>
  </div>
</template>