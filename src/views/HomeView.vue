<template>
  <div class="d-flex cards__wrapper justify-center">
    <CardList title="Lista doméstica" text="Limpar a casa"/>
    <CardList title="Faculdade" text="Trabalho de programação"/>
    <CardList title="Trabalho" text="Implementação"/>
  </div>

  <v-btn elevation="3" icon fab class="add-button position-absolute" @click="openDialog">
    <v-icon>mdi-plus</v-icon>
  </v-btn>

  <DialogCreateCard ref="createDialog"/>
</template>

<script>
import { defineComponent } from 'vue';
import CardList from '../components/CardList.vue';
import DialogCreateCard from '@/components/DialogCreateCard.vue';

export default defineComponent({
  name: 'HomeView',
  components: {
    CardList,
    DialogCreateCard,
  },
  methods: {
    openDialog() {
      this.$refs.createDialog.dialog = true;
    }
  }
});
</script>

<style>
  .add-button {
    right: 20px;
    bottom: 20px;
  }

  .cards__wrapper {
    gap: 15px;
  }
</style>