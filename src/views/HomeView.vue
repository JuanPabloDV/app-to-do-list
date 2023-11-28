<template ref="home">
  <v-container class="d-flex cards__wrapper justify-center">
    <v-row class="d-flex justify-center">
      <v-col class="d-flex justify-center" cols="3" v-for="list of allList" :key="list.id">
        <CardList :id="list.id" :title="list.title" :description="list.description" :completed="list.isCompleted"/>
      </v-col>
    </v-row>
  </v-container>

  <v-btn elevation="3" icon fab class="add-button position-absolute" @click="openDialog">
    <v-icon>mdi-plus</v-icon>
  </v-btn>

  <DialogCreateCard ref="createDialog"/>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue';
import CardList from '../components/CardList.vue';
import DialogCreateCard from '@/components/DialogCreateCard.vue';
import api from '@/plugins/api';

export default defineComponent({
  name: 'HomeView',
  data () {
    return {
    }
  },
  components: {
    CardList,
    DialogCreateCard,
  },
  methods: {
    openDialog() {
      this.$refs.createDialog.dialog = true;
    },
  },
  setup() {
    const allList = ref([]);

    const fetchTodo = async () => {
      try {
        const response = await api.get('/todo');
        allList.value = response.data;
      } catch (error) {
        console.error('Erro ao buscar dados da API:', error);
      }
    };

    onMounted(fetchTodo);

    return {
      allList,
    };
  },
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