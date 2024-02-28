<script setup>
import { reactive, ref, watch } from "vue";

const dados = reactive({
  numero1: 0,
  numero2: 0,
});

const operacao = ref("");
const resultado = ref(0);

watch([() => dados.numero1, () => dados.numero2], calcularResultado);

function calcularResultado() {
  if (!operacao.value) return;
  switch (operacao.value) {
    case "+":
      resultado.value = dados.numero1 + dados.numero2;
      break;
    case "-":
      resultado.value = dados.numero1 - dados.numero2;
      break;
    case "*":
      resultado.value = dados.numero1 * dados.numero2;
      break;
    case "/":
      resultado.value = dados.numero1 / dados.numero2;
      break;
  }
}
</script>

<template>
  <div class="calculator-container">
    <div class="calculator-card">
      <header>
        <h1>Calculadora aritmética</h1>
        <hr />
      </header>
      <div class="input-container">
        <label for="operacao">Escolha a operação</label>
        <select id="operacao" v-model="operacao" @change="calcularResultado">
          <option disabled value="">Escolha um item</option>
          <option>+</option>
          <option>-</option>
          <option>*</option>
          <option>/</option>
        </select>
      </div>
      <div class="input-container">
        <label for="numero1">Número 1</label>
        <input
          type="number"
          id="numero1"
          v-model.number="dados.numero1"
          @input="calcularResultado"
        />
      </div>
      <div class="input-container">
        <label for="numero2">Número 2</label>
        <input
          type="number"
          id="numero2"
          v-model.number="dados.numero2"
          @input="calcularResultado"
        />
      </div>
      <div class="resultado" v-if="operacao">
        Resultado: <span>{{ resultado }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.calculator-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(to bottom right, violet, navy);
}

.calculator-card {
  width: 400px;
  padding: 20px;
  background-color: white;
  border-radius: 15px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

.input-container {
  margin-bottom: 15px;
}

.input-container label {
  display: block;
  margin-bottom: 5px;
}

.input-container input,
.input-container select {
  width: 85%;
  padding: 8px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.resultado {
  color: green;
  margin-top: 10px;
}
</style>
