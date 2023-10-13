<template>
  <div style="margin: 5em">
    <h1 style="font-size: 3rem">Editar Despesa</h1>
    <div-container>
      <q-card>
        <q-card-section>
          <q-input v-model="editedExpense.data" label="Data" />
        </q-card-section>
        <q-card-section>
          <q-input v-model="editedExpense.descricao" label="Descrição" />
        </q-card-section>
        <q-card-section>
          <q-input v-model="editedExpense.valor" label="Valor" />
        </q-card-section>
        <q-card-section>
          <q-input v-model="editedExpense.user.name" label="Empresa" readonly />
        </q-card-section>
        <q-card-actions align="right">
          <q-btn label="Cancelar" @click="cancelEdit" />
          <q-btn label="Salvar" color="primary" @click="saveExpense" />
        </q-card-actions>
      </q-card>
    </div-container>
  </div>
  <loading-modal></loading-modal>
</template>

<script>
import { axiosInstance } from "src/axios";
import LoadingModal from "src/components/LoadingModal.vue";

export default {
  components: {
    LoadingModal,
  },
  data() {
    return {
      editedExpense: {
        data: "",
        descricao: "",
        valor: "",
        empresa: "",
        user: "",
      },
      isLoading: false,
    };
  },
  methods: {
    // Carregar as informações da despesa com a ID clicada
    loadExpenseData() {
      const expenseId = this.$route.params.id;

      axiosInstance
        .get(`/despesas/${expenseId}`)
        .then((response) => {
          this.editedExpense = response.data;
          this.isLoading = true;
        })
        .catch((error) => {
          console.error(error);
          this.isLoading = true;
        });
    },
    saveExpense() {
      axiosInstance
        .put(`/despesas/${this.$route.params.id}/atualizar`, this.editedExpense)
        .then((response) => {
          console.log("Despesa atualizada com sucesso.");
          this.$router.push("/despesas");
        })
        .catch((error) => {
          console.error(error);
        });
    },
    cancelEdit() {
      this.$router.push("/despesas");
    },
  },
  created() {
    // Carregar os dados da despesa ao entrar na página
    this.loadExpenseData();
  },
};
</script>
