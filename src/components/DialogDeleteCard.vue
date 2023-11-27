<template>
    <v-dialog v-model="dialog" width="auto">
      <v-card>
        <v-card-title>Excluir</v-card-title>
        <v-card-text>
          <p>Deseja excluir a tarefa?</p>
        </v-card-text>
        <v-card-actions class="d-flex justify-center">
          <v-btn color="black" @click="dialog = false">Cancelar</v-btn>
          <v-btn color="red">Excluir</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
export default {
  data () {
    return {
        dialog: false,
    }
  },
}
</script>