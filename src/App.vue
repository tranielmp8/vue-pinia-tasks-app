<template>
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo">
      <!-- remember we created a name called Yoshi in the TaskStore.js -->
      <h1>Pinia Tasks</h1>
    </header>

    <!-- New Task Form -->
    <div class="new-taks-form">
      <TaskForm />
    </div>

    <!-- filter button -->
    <nav class="filter" >
      <button @click="filter = 'all'" >All Tasks</button>
      <button @click="filter = 'favs'" >Favorite Tasks</button>
    </nav>

    <!-- Task List -->
    <div class="task-list" v-if="filter === 'all'" >
      <p>you have {{ taskStore.totalCount }} tasks left to do</p>
      <div v-for="task in taskStore.tasks" >
        <TaskDetails :task="task" />
      </div>
    </div>
    <div class="task-list" v-if="filter === 'favs'">
      <p>you have {{ taskStore.favCount }} Favs left to do</p>
      <div v-for="task in taskStore.favs" >
        <TaskDetails :task="task" />
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from 'vue'
import TaskDetails from './components/TaskDetails.vue'
import TaskForm from './components/TaskForm.vue'
import {useTaskStore} from './stores/TaskStore'
  export default {
    components: { TaskDetails, TaskForm },
    setup(){
      const filter = ref('all')
      const taskStore = useTaskStore()

      return { taskStore, filter }
    }
  }
</script>