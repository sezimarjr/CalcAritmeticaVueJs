<script setup>
import { reactive } from "vue";

const estado = reactive({
  pNumero: "",
  sNumero: "",
  operacoes: {
    soma: (a, b) => a + b,
    subtracao: (a, b) => a - b,
    multiplicacao: (a, b) => a * b,
    divisao: (a, b) => (b !== 0 ? a / b : "Divisão por Zero"),
  },
  resultado: 0,
});

const calcularResultado = () => {
  const { pNumero, sNumero, operacaoAritmetica } = estado;
  estado.resultado = estado.operacoes[operacaoAritmetica](
    parseFloat(pNumero),
    parseFloat(sNumero)
  );
};
</script>

<template>
  <div class="container">
    <h1>Calculadora Aritmetica VueJs</h1>

    <input
      v-model="estado.pNumero"
      type="text"
      placeholder="Digite o primeiro numero"
      @input="calcularResultado"
    />

    <input
      v-model="estado.sNumero"
      type="text"
      placeholder="Digite o segundo numero"
      @input="calcularResultado"
    />
    <select v-model="estado.operacaoAritmetica" @change="calcularResultado">
      <option value="soma">Somar</option>
      <option value="subtracao">Subtração</option>
      <option value="multiplicacao">Multiplicação</option>
      <option value="divisao">Divisão</option>
    </select>
    <p v-if="!isNaN(estado.resultado)">{{ estado.resultado }}</p>
    <p v-else></p>
  </div>
</template>

<style scoped>
.container {
  max-width: 420px;
  margin: 0 auto;
  padding: 20px;
  background-color: #d7d8e0;
  border-radius: 5px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
input {
  margin-bottom: 8px;
}
select {
  text-align: center;
}
</style>
