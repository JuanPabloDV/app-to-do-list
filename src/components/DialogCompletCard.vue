<template>
    <v-dialog v-model="dialog" width="auto">
      <v-card>
        <v-card-title>Concluir</v-card-title>
        <v-card-text>
          <p>Deseja concluir a tarefa?</p>
        </v-card-text>
        <v-card-actions class="d-flex justify-center">
          <v-btn color="black" @click="dialog = false">Cancelar</v-btn>
          <v-btn color="red" @click="completItem">Concluir</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
import api from '@/plugins/api';

export default {
  data () {
    return {
        dialog: false,
        id: 0,
    }
  },
  methods: {
    async completItem() {
      try {
        await api.put('/todo/' + this.id, {
          isCompleted: true,
        });

        this.dialog = false;
        window.location.reload();
      } catch (error) {
        console.error('Erro ao atualizar o item:', error);
      }
    },
  }
}
</script>