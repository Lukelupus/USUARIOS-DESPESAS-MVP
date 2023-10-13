<template>
  <div style="margin: 5em">
    <h1 style="font-size: 3rem">Lista de Usuários</h1>
    <q-table :rows="usuarios" :columns="columns">
      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td key="nome">{{ props.row.name }}</q-td>
          <q-td key="email">{{ props.row.email }}</q-td>
          <q-td key="acoes">
            <q-btn @click="editarUsuario(props.row.id)" label="Editar" />
            <q-btn
              @click="excluirUsuario(props.row.id)"
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
      usuarios: [], // Array para armazenar os usuários
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
    editarUsuario(id) {
      this.$router.push(`/usuarios/${id}`);
    },
    excluirUsuario(id) {
      this.$axios
        .delete(`users/${id}`)
        .then((response) => {
          console.log("Usuário excluído com sucesso:", response.data);
          // Atualizar a lista de usuários após a exclusão
          this.buscarUsuarios();
        })
        .catch((error) => {
          console.error("Erro ao excluir usuário:", error);
        });
    },
    buscarUsuarios() {
      // Implemente a lógica para buscar a lista de usuários da sua API Laravel
      this.$axios
        .get("users")
        .then((response) => {
          this.usuarios = response.data;
        })
        .catch((error) => {
          console.error("Erro ao buscar usuários:", error);
        });
    },
  },
  mounted() {
    axiosInstance
      .get("/usuarios")
      .then((response) => {
        this.usuarios = response.data;
      })
      .catch((error) => {
        console.error("Erro ao buscar usuários:", error);
      });
  },
};
</script>
