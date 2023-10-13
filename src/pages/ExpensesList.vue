<template>
  <div style="margin: 5em">
    <h1 style="font-size: 3rem">Lista de Despesas Cadastradas</h1>
    <q-table :rows="despesas" :columns="columns">
      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="data">{{ props.row.data }}</q-td>
          <q-td key="descricao">{{ props.row.descricao }}</q-td>

          <q-td key="descricao">{{ props.row.valor }}</q-td>
          <q-td key="data">{{ props.row.user.name }}</q-td>

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
          name: "data",
          required: true,
          label: "Data Da Despesa",
          align: "left",
          field: "data",
          sortable: true,
        },
        {
          name: "Descrição",
          required: true,
          label: "Descrição",
          align: "left",
          field: "descricao",
          sortable: true,
        },
        {
          name: "Valor",
          label: "Valor",
          align: "left",
        },
        {
          name: "email",
          label: "Empresa",
          align: "left",
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
      this.$router.push(`/despesas/edit/${id}`);
    },
    excluirDespesa(id) {
      axiosInstance
        .delete(`despesas/${id}/excluir`)
        .then((response) => {
          console.log(response.data);

          this.buscardespesas();
        })
        .catch((error) => {
          console.error(error);
        });
    },
    buscardespesas() {
      axiosInstance
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
