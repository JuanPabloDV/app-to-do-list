<template>
    <v-dialog v-model="dialog" width="auto">
      <v-card>
        <v-card-title>Excluir</v-card-title>
        <v-card-text>
          <p>Deseja excluir a tarefa?</p>
        </v-card-text>
        <v-card-actions class="d-flex justify-center">
          <v-btn color="black" @click="dialog = false">Cancelar</v-btn>
          <v-btn color="red" @click="deleteItem">Excluir</v-btn>
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
    }
  },
  props: {
    id: String,
  },
  methods: {
    async deleteItem() {
      try {
        await api.delete('/todo/' + this.$props.id);
        window.location.reload();
      } catch (error) {
        console.error('Erro ao excluir o item:', error);
      }
    },
  }
}
</script>