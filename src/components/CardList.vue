<template>
  <div class="position-relative">
    <svg-icon v-if="completed" class="position-absolute card__icon" color="green" size="40" type="mdi" :path="completIcon"></svg-icon>
    <v-card class="cards position-relative" elevation="3">
      <v-card-title class="d-flex justify-center">{{ title }}</v-card-title>
      <v-card-text class="d-flex justify-center my-5">
        <ul>
          <li>{{ description }}</li>
        </ul>
      </v-card-text>
      <v-card-actions class="d-flex justify-center">
        <v-btn v-if="!completed" @click="completCard"><svg-icon size="30" color="green" type="mdi" :path="completIcon"></svg-icon></v-btn>
        <v-btn v-if="!completed" @click="editCard"><svg-icon size="30" type="mdi" :path="editIcon"></svg-icon></v-btn> 
        <v-btn color="red" @click="deletCard"><svg-icon size="30" type="mdi" :path="trashIcon"></svg-icon></v-btn>
      </v-card-actions>
    </v-card>

    <DialogDeleteCard ref="deletedDialog" :id="id"/>
    <DialogCreateCard ref="createDialog" :id="id" :title="title" :description="description"/>
    <DialogCompletCard ref="completDialog" :id="id"/>
  </div>    
</template>

<script>
import DialogDeleteCard from './DialogDeleteCard.vue';
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiCheck, mdiTrashCanOutline, mdiPencilOutline } from '@mdi/js';
import DialogCreateCard from './DialogCreateCard.vue';
import DialogCompletCard from './DialogCompletCard.vue';

export default {
  name: 'cardList',
  components: {
    DialogDeleteCard,
    DialogCompletCard,
    SvgIcon,
    DialogCreateCard,
},
  data() {
		return { 
      completIcon: mdiCheck,
      trashIcon: mdiTrashCanOutline,
      editIcon: mdiPencilOutline, 
		}
	},
  props: {
    id: String,
    title: String,
    description: String,
    completed: Boolean,
  },
  methods: {
    completCard() {
      console.log(this.$refs.completDialog.dialog)
      this.$refs.completDialog.dialog = true;
      this.$refs.completDialog.id = this.id;
    },
    editCard() {
      this.$refs.createDialog.dialog = true;
      this.$refs.createDialog.id = this.id;
      this.$refs.createDialog.title = this.title;
      this.$refs.createDialog.description = this.description;
    },
    deletCard() {
      this.$refs.deletedDialog.dialog = true;
    },
  },
}
</script>

<style>
  .cards {
    width: 250px;
    padding: 0 10px;
  }

  .card__icon {
    top: 0;
    right: 0;
    z-index: 1;
  }
</style>
