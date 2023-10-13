<template>
  <div style="margin: 5em">
    <h1 style="font-size: 3rem">Editar Usuário</h1>

    <div>
      <h2 style="font-size: 2rem">Informações do Usuário</h2>
      <p style="font-size: 1.25rem"><strong>Nome:</strong> {{ user.name }}</p>
      <p style="font-size: 1.25rem"><strong>Email:</strong> {{ user.email }}</p>
    </div>

    <h2 style="font-size: 2rem">Despesas do Usuário</h2>

    <div>
      <table style="width: 100%">
        <thead>
          <tr>
            <th>Data</th>
            <th>Descrição</th>
            <th>Valor</th>
          </tr>
        </thead>
        <tbody>
          <tr
            style="text-align: center"
            v-for="despesa in despesas"
            :key="despesa.id"
          >
            {{
              console.log("Logging item:", despesa.data)
            }}
            <td>{{ despesa.data }}</td>
            <td>{{ despesa.descricao }}</td>
            <td>{{ despesa.valor }}</td>
            <q-btn label="Voltar" @click="cancelEdit" />
            <q-btn
              @click="editarDespesa(despesa.id)"
              style="background-color: rgb(86, 213, 218); margin: 1em"
              label="Editar"
            />
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { axiosInstance } from "src/axios";

export default {
  data() {
    return {
      id: null,
      user: {},
      despesas: [],
    };
  },
  methods: {
    loadUser() {
      axiosInstance
        .get(`/usuarios/${this.$route.params.id}`)
        .then((response) => {
          this.user = response.data;
        })
        .catch((error) => {
          console.error("Erro ao carregar informações do usuário:", error);
        });
    },
    loadExpenses() {
      axiosInstance
        .get(`/usuarios/${this.$route.params.id}/despesas`)
        .then((response) => {
          this.despesas = response.data;
        })
        .catch((error) => {
          console.error("Erro ao carregar despesas do usuário:", error);
        });
    },
    cancelEdit() {
      this.$router.push("/usuarios");
    },
    editarDespesa(id) {
      this.$router.push(`/despesas/edit/${id}`);
    },
  },
  mounted() {
    this.loadUser();
    this.loadExpenses();
    console.log(this.despesas);
  },
};
</script>
