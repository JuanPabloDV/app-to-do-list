<template>
  <div>
    <v-card class="cards" elevation="3">
      <v-card-title class="d-flex justify-center">{{ title }}</v-card-title>
      <v-card-tex class="d-flex justify-center my-5">
        <ul>
          <li>{{ text }}</li>
        </ul>
      </v-card-tex>
      <v-card-actions class="d-flex justify-center">
        <v-btn>Editar</v-btn>
        <v-btn color="red" @click="openDialog">Excluir</v-btn>
      </v-card-actions>
    </v-card>

    <DialogDeleteCard ref="deletedDialog"/>
  </div>    
</template>

<script>
import DialogDeleteCard from './DialogDeleteCard.vue';

export default {
  name: 'cardList',
  components: {
    DialogDeleteCard
  },
  props: {
    title: String,
    text: String,
  },
  methods: {
    openDialog() {
      this.$refs.deletedDialog.dialog = true;
    }
  }
}
</script>

<style>
  .cards {
    width: 250px;
    padding: 0 10px;
  }
</style>
