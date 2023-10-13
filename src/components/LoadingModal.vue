<template>
  <q-dialog v-model="showLoading" persistent>
    <q-card>
      <q-card-section>
        <q-spinner-gears size="70px" color="primary" />
      </q-card-section>
      <q-card-section>
        <div class="text-h6">Carregando...</div>
      </q-card-section>
    </q-card>
  </q-dialog>
</template>

<script>
export default {
  data() {
    return {
      showLoading: false,
    };
  },
};
</script>
