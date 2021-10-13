<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Codebrains Todos</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-refresher slot="fixed" @ionRefresh="refresh($event)">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>
      
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Codebrains Todos</ion-title>
        </ion-toolbar>
      </ion-header>
      
      <TodoForm />
      <ion-list>
        <TodoListItem v-for="todo in todos" :key="todo.id" :todo="todo"/>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonList, IonPage, IonRefresher, IonRefresherContent, IonTitle, IonToolbar } from '@ionic/vue';
import TodoListItem from '@/components/TodoListItem.vue';
import TodoForm from '@/components/TodoForm.vue';
import { defineComponent, onMounted, ref } from 'vue';
import { getMessages } from '@/data/messages';
import { findAllTodos } from '@/data/todos';
export default defineComponent({
  name: 'Home',
  data() {
    return {
      messages: getMessages()
    }
  },
  methods: {
    refresh: (ev: CustomEvent) => {
      setTimeout(() => {
        ev.detail.complete();
      }, 3000);
    }
  },
  components: {
    IonContent,
    IonHeader,
    IonList,
    IonPage,
    IonRefresher,
    IonRefresherContent,
    IonTitle,
    IonToolbar,
    TodoListItem,
    TodoForm
  },
  setup() {
    /*const todos = ref([]);
    const response = await findAllTodos();
    todos.value = response.data;
    
    return {
      todos
    }*/
    const todos = ref([]);
    onMounted(async () => {
      const response = await findAllTodos();
      todos.value = response.data;
    });

    return {
      todos
    }
  }
});
</script>