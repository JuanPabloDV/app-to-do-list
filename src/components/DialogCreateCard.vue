<template>
    <v-dialog v-model="dialog" width="400px">
      <v-card>
        <v-card-title>Adicionar tarefa</v-card-title>
        <v-card-text>
            <v-text-field variant="outlined" clearable label="Título"/>
            <v-text-field variant="outlined" clearable label="Tarefa"/>
        </v-card-text>
        <v-card-actions class="d-flex justify-center">
          <v-btn color="black" @click="dialog = false">Cancelar</v-btn>
          <v-btn color="red">Adicionar</v-btn>
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