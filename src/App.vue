<template>
  <div>
    <h2>Ma To-Do List</h2>

    <input v-model="newTask" placeholder="Ajouter une tâche">
    <button @click="addTask">Ajouter</button>
    <button @click="clearAll">Tout supprimer</button>

    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <span 
          :class="{ done: task.done }"
          @click="toggleTask(index)"
          style="cursor:pointer"
        >
          {{ task.text }}
        </span>

        <button @click="removeTask(index)">Supprimer</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: []
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() === "") {
        alert("Champ vide !");
        return;
      }

      this.tasks.push({
        text: this.newTask,
        done: false
      });

      this.newTask = "";
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    clearAll() {
      this.tasks = [];
    },
    toggleTask(index) {
      this.tasks[index].done = !this.tasks[index].done;
    }
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
  color: gray;
}
</style>