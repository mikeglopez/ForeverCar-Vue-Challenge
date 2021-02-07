<script>
import Task from '@/components/Task'
import data from '@/mock-api.js'

export default {
  name: 'List',
  components: { Task },
  data: () => ({
    allTasks: data.tasks,
    input: '',
    filter: false
  }),
  methods: {
    addTask() {
      if (this.input.length) {
        this.allTasks.push({ name: this.input });
        this.input = '';
      }
    },
    filterTasks() {
      if (this.input.length) {
        this.filter = !this.filter;
      }
    },
    removeTask(taskName) {
      const index = this.allTasks.map((task) => task.name).indexOf(taskName)
      this.allTasks.splice(index, 1);
    },
    toggleCompleted(taskName) {
      const index = this.allTasks.map((task) => task.name).indexOf(taskName)
      let task = this.allTasks[index];
      task.completed = !task.completed;

      const updatedTasks = this.allTasks.slice();
      updatedTasks.splice(index, 1);
      task.completed ? updatedTasks.push(task) : updatedTasks.unshift(task);

      this.allTasks = updatedTasks;
    }
  },
  computed: {
    displayedTasks() {
      let tasksToDisplay = this.allTasks;
      if (this.filter) {
        tasksToDisplay = this.allTasks.filter(task => task.name.toLowerCase().includes(this.input.toLowerCase()));
      }
      return tasksToDisplay;
    }
  }
}
</script>

<template>
  <v-form>
    <v-card max-width='80%' class='mx-auto mt-4 pa-8'>
      <v-row>

        <!-- Text Field -->
        <v-col cols='8'>
          <v-text-field
            v-model='input'
            label='New Task'
          >
          </v-text-field>
        </v-col>

        <!-- Add Button -->
        <v-col cols='2' class='text-center'>
          <v-btn large color='info' @click='addTask'>Add Task</v-btn>
        </v-col>

        <!-- Filter Button -->
        <v-col cols='2' class='text-center'>
          <v-btn large :color='this.filter ? "success" : "info"' @click='filterTasks'>Filter Tasks</v-btn>
        </v-col>

      </v-row>
      <v-row>

        <!-- Task List -->
        <v-col cols='12'>
          <div
            v-for='( task, i ) in this.displayedTasks'
            :key='i'
          >

            <v-row class='task-row'>
              <!-- Task -->
              <v-col cols='10'>
                <Task :complete='task.completed' :name='task.name' />
              </v-col>

              <!-- Complete Button -->
              <v-col cols='1' class='text-center'>
                <v-btn :color='task.completed ? "info" : ""' fab small @click='toggleCompleted(task.name)'><v-icon>mdi-check</v-icon></v-btn>
              </v-col>

              <!-- Remove Button -->
              <v-col cols='1' class='text-center'>
                <v-btn color='error' fab small @click='removeTask(task.name)'><v-icon>mdi-close</v-icon></v-btn>
              </v-col>
            </v-row>

          </div>
        </v-col>

      </v-row>
    </v-card>
  </v-form>
</template>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
.task-row {
  margin: 20px 0;
}
</style>
