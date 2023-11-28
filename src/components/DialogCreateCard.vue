<template>
  <v-form>
    <v-dialog v-model="dialog" width="400px">
      <v-card>
        <v-card-title>{{ id === 0 ? 'Adicionar tarefa' : 'Editar tarefa' }}</v-card-title>
        <v-card-text>
          <div class="position-relative">
            <v-text-field v-model="title" variant="outlined" clearable label="Título"/>
            <p v-show="warningTitle" class="position-absolute warning-card">Campo obrigatório</p>
          </div>
          <div class="position-relative">
            <v-text-field v-model="description" variant="outlined" clearable label="Tarefa"/>
            <p v-show="warningDescription" class="position-absolute warning-card">Campo obrigatório</p>
          </div>
        </v-card-text>
        <v-card-actions class="d-flex justify-center">
          <v-btn color="black" @click="dialog = false">Cancelar</v-btn>
          <v-btn v-if="id === 0" color="red" @click="createItem">Adicionar</v-btn>
          <v-btn v-else color="red" @click="editItem">Editar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-form>
</template>

<script>
import api from '@/plugins/api';

export default {
  data () {
    return {
        dialog: false,
        id: 0,
        title: null,
        description: null,
        warningTitle: false,
        warningDescription: false,
    }
  },
  methods: {
    async editItem() {
      console.log(this.title)
      if (this.title === null || this.title === '' || this.description === null || this.description === '') {
        if (this.title === null || this.title === '') {
          this.warningTitle = true;
        }

        if (this.description === null || this.description === '') {
          this.warningDescription = true;
        }
      } else {
        try {
          await api.put('/todo/' + this.id, {
            title: this.title,
            description: this.description,
          });

          window.location.reload();
        } catch (error) {
          console.error('Erro ao atualizar o item:', error);
        }
      }  
    },
    async createItem() {
      if (this.title === null || this.title === '' || this.description === null || this.description === '') {
        if (this.title === null || this.title === '') {
          this.warningTitle = true;
        }

        if (this.description === null || this.description === '') {
          this.warningDescription = true;
        }
      } else {
        try {
          await api.post('/todo/', {
            title: this.title,
            description: this.description,
          });

          this.dialog = false;
          window.location.reload();
        } catch (error) {
          console.error('Erro ao criar o item:', error);
        }
      }
    },
  },
}
</script>

<style>
  .warning-card {
    bottom: 5px;
    font-size: 10px;
    color: red;
  }
</style>