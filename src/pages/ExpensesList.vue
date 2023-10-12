<template>
  <div>
    <h1>Lista de Despesas Cadastradas</h1>
    <q-table :rows="despesas" :columns="columns">
      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="nome">{{ props.row.name }}</q-td>
          <q-td key="email">{{ props.row.email }}</q-td>

          <q-td key="descricao">{{ props.row.descricao }}</q-td>
          <q-td key="data">{{ props.row.data }}</q-td>

          <q-td key="acoes">
            <q-btn @click="editarDespesa(props.row.id)" label="Editar" />
            <q-btn
              @click="excluirDespesa(props.row.id)"
              label="Excluir"
              color="negative"
            />
          </q-td>
        </q-tr>
      </template>
    </q-table>
  </div>
</template>

<script>
import { axiosInstance } from "src/axios";

export default {
  data() {
    return {
      despesas: [], // Array para armazenar os usuários
      columns: [
        {
          name: "nome",
          required: true,
          label: "Nome",
          align: "left",
          field: "nome",
          sortable: true,
        },
        {
          name: "email",
          required: true,
          label: "E-mail",
          align: "left",
          field: "email",
          sortable: true,
        },
        {
          name: "acoes",
          label: "Ações",
          align: "left",
        },
      ],
    };
  },
  methods: {
    editarDespesa(id) {
      this.$router.push(`/despesas/${id}`);
    },
    excluirDespesa(id) {
      this.$axios
        .delete(`despesas/${id}`)
        .then((response) => {
          console.log("Usuário excluído com sucesso:", response.data);
          // Atualizar a lista de usuários após a exclusão
          this.buscardespesas();
        })
        .catch((error) => {
          console.error("Erro ao excluir usuário:", error);
        });
    },
    buscardespesas() {
      // Implemente a lógica para buscar a lista de usuários da sua API Laravel
      this.$axios
        .get("despesas")
        .then((response) => {
          this.despesas = response.data;
        })
        .catch((error) => {
          console.error("Erro ao buscar usuários:", error);
        });
    },
  },
  mounted() {
    axiosInstance
      .get("/despesas")
      .then((response) => {
        this.despesas = response.data;
      })
      .catch((error) => {
        console.error("Erro ao buscar usuários:", error);
      });
  },
};
</script>
