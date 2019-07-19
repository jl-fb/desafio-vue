<template>
  <div class="form">
    <form action="#" class="col-lg-10 mt-3 d-block">
      <div class="form-group row">
        <label for="estado" class="col-8 col-sm-2 m-auto btn btn-success">Digite o estado:</label>
        <b-form-input
          id="estado"
          v-model="nome"
          type="text"
          class="form-control col-11 col-sm-9"
          placeholder="Digite o nome do Estado..."
        />
        <button id="enviar" class="btn btn-primary m-auto" @click.prevent="loadEstados">Enviar</button>
      </div>
      <div class="resp mt-5">
        <b-table
          v-if="estado && erro === false"
          class="table-dark text-center"
          :items="estado"
          :fields="campos"
        ></b-table>
        <b-alert v-show="erro === true" variant="danger" show dismissible>
          Estado não encontrado! Estado digitado:
          <b>&rArr;</b>
          {{nome}}
        </b-alert>
      </div>
    </form>
  </div>
</template>

<script>
import listaEstados from "../assets/estados";
import comparaString from "string-similarity";
export default {
  name: "Form",
  data() {
    return {
      nome: null,
      erro: false,
      estado: null,
      estados: listaEstados,
      campos: [
        { key: "sigla", label: "Sigla" },
        { key: "nome", label: "Nome" },
        { key: "capital", label: "Capital" },
        { key: "regiao", label: "Região" }
      ]
    };
  },
  methods: {
    loadEstados() {
      let indiceIgualdade = [];
      for (let i in listaEstados) {
        indiceIgualdade = comparaString.compareTwoStrings(
          this.nome.toUpperCase(),
          listaEstados[i].nome.toUpperCase()
        );
        if (indiceIgualdade >= 0.5) {
          this.estado = [listaEstados[i]];
        }
      }

      // Por algum motivo que não descobri esse código abaixo não funcionou como o esperado

      /* for (let i = 0; i < listaEstados.length; i++) {
        const indiceIgualdade = comparaString.compareTwoStrings(
          this.nome.toUpperCase(),
          listaEstados[i].nome.toUpperCase()
        );
        if (indiceIgualdade >= 0.5) {
          this.estado = [listaEstados[i]];
          this.erro = false;
        } else {
          this.erro = true
        }
      } */
    }
  }
};
</script>

<style>
form {
  margin: auto;
}
</style>
