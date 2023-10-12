<template>
  <div>
    <container>
      <form @submit="updateExpense">
        <input v-model="expense.description" label="Descrição" floating-label />
        <input
          v-model="expense.value"
          label="Valor"
          floating-label
          type="number"
        />
        <input v-model="expense.date" label="Data" floating-label type="date" />
        <btn label="Atualizar Despesa" color="primary" type="submit" />
      </form>
    </container>
  </div>
</template>

<script>
import { axiosInstance } from "src/axios";
export default {
  data() {
    return {
      expense: {
        id: null,
        description: "",
        value: 0,
        date: "",
      },
    };
  },

  methods: {
    fetchExpense() {
      const expenseId = this.$route.params.id;

      axiosInstance
        .get(`/despesas/${expenseId}`)
        .then((response) => {
          this.expense = response.data;
        })
        .catch((error) => {
          console.error("Erro ao buscar os detalhes da despesa", error);
        });
    },
    // Método para atualizar a despesa
    updateExpense() {
      const expenseId = this.$route.params.id;

      axiosInstance
        .put(`/despesas/${expenseId}`, this.expense)
        .then(() => {
          this.$router.push("/despesas");
        })
        .catch((error) => {
          console.error("Erro ao atualizar a despesa", error);
        });
    },
  },
  created() {
    this.fetchExpense();
  },
};
</script>
