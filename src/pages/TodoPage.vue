<template>
  <q-page class="q-pa-xl bg-grey-1 column">
    <div class="row q-pa-sm">
      <q-input bottom-slots v-model="newTask" placeholder="add task" dense>
        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-grey-1" separator>
      <q-item
        tag="label"
        val="teal"
        v-for="(task, index) in tasks"
        :key="task.index"
        :class="{ 'done bg-green-2': task.done }"
        v-ripple
      >
        <!-- @click="task.done = !task.done" -->
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary" />
        </q-item-section>

        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>

        <q-item-section side>
          <q-btn
            flat
            round
            icon="delete"
            color="blue-10"
            @click.stop="deleteTask(index)"
          />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { useQuasar } from "quasar";
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },
  methods: {
    deleteTask(index) {
      confirm("do you want to delete this task?")
        ? this.tasks.splice(index, 1)
        : console.log("task is not deleted");
    },
    addTask() {
      this.tasks.push({
        title: this.newTask,
        done: false,
      });
      alert("new task added");
      this.newTask = "";
    },
  },
};
</script>

<!-- <script setup>
const tasks = [
  {
    title: "one",
    done: false,
  },
  {
    title: "twi",
    done: false,
  },
  {
    title: "three",
    done: false,
  },
];

const deleteTask = (index) => {
  tasks.splice(index, 1);
  alert("task deleted");
};
</script> -->

<style scoped>
.done {
  text-decoration: line-through;
  opacity: 0.3;
}
:q-item__label {
  text-decoration: line-through;
}

.q-input {
  width: 100%;
}
</style>
