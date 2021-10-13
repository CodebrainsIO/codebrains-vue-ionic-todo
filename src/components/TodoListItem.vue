<template>
  <ion-item v-if="todo" :detail="false" class="list-item">
    <div slot="start" :class="!todo.completed ? 'dot dot-unread' : 'dot'"></div>
    <ion-label class="ion-text-wrap">
      <h2 :class="!todo.completed ? 'uncompleted' : 'completed'">
        {{ todo.title }}
      </h2>
    </ion-label>
    <ion-toggle :checked="todo.completed"></ion-toggle>
    <ion-button color="danger">X</ion-button>
  </ion-item>
</template>

<script lang="ts">
import { IonItem, IonLabel, IonButton, IonToggle } from "@ionic/vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "TodoListItem",
  components: {
    IonItem,
    IonLabel,
    IonButton,
    IonToggle,
  },
  props: {
    todo: Object,
  },
  setup() {
    const clickedStar = () => {
      console.log("Star clicked!");
    };

    return { clickedStar }
  },
});
</script>

<style scoped>
.list-item {
  --padding-start: 0;
  --inner-padding-end: 0;
}

.list-item ion-label {
  margin-top: 12px;
  margin-bottom: 12px;
}

.list-item h2 {
  font-weight: 600;
  margin: 0;
}

.list-item p {
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  width: 95%;
}

.list-item .date {
  float: right;
  align-items: center;
  display: flex;
}

.list-item ion-icon {
  color: #c9c9ca;
}

.list-item ion-note {
  font-size: 15px;
  margin-right: 8px;
  font-weight: normal;
}

.list-item ion-note.md {
  margin-right: 14px;
}

.list-item .dot {
  display: block;
  height: 12px;
  width: 12px;
  border-radius: 50%;
  align-self: start;
  margin: 16px 10px 16px 16px;
}

.list-item .dot-unread {
  background: var(--ion-color-primary);
}

ion-toggle {
  margin-right: 15px;
}

ion-button {
  margin-right: 10px;
}

.completed {
  text-decoration: line-through;
}
</style>
