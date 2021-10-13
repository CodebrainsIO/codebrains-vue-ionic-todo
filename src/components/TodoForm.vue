<template>
    <ion-grid class="input-grid">
    <form @submit.prevent>
      <ion-row>
        <ion-col size="9">
          <ion-input
            placeholder="Enter Todo"
            v-model="title"
          ></ion-input>
        </ion-col>
        <ion-col size="3">
          <ion-button type="submit" color="primary" @click="onSubmit($event)">Add</ion-button>
        </ion-col>
      </ion-row>
    </form>
  </ion-grid>
</template>

<script lang="ts">
import { IonGrid, IonRow, IonCol, IonInput, IonButton } from '@ionic/vue';
import { defineComponent, ref } from 'vue'

export default defineComponent({
    name: 'TodoForm',
    components: {
        IonGrid,
        IonRow,
        IonCol,
        IonInput,
        IonButton
    },
    props: {
        submitTodo: {
            type: Function,
            required: true
        }
    },
    setup(props){
        const title = ref('');
        const onSubmit = (event: any) => {
            console.log("Submit", title.value);
            props.submitTodo({title: title.value, completed: false})
            title.value = '';
        }

        return {
            title,
            onSubmit
        }
    }
})
</script>
