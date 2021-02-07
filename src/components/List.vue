<script>
import Task from '@/components/Task'
import data from '@/mock-api.js'

export default {
  name: 'List',
  components: { Task },
  data: () => ({
    tasks: data.tasks,
    input: ''
  }),
  methods: {
    addTask() {
      if (this.input.length) {
        this.tasks.push({ name: this.input });
        this.input = '';
      }
    },
    removeTask(task) {
      this.tasks.splice(task, 1);
    },
    toggleCompleted(index) {
      let task = this.tasks[index];
      task.completed = !task.completed;

      const updatedTasks = this.tasks.slice();
      updatedTasks.splice(index, 1);
      task.completed ? updatedTasks.push(task) : updatedTasks.unshift(task);

      this.tasks = updatedTasks;
    }
  }
}
</script>

<template>
  <v-form>
    <v-card max-width='80%' class='mx-auto mt-4 pa-8'>
      <v-row>

        <!-- Text Field -->
        <v-col cols='10'>
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

      </v-row>
      <v-row>

        <!-- Task List -->
        <v-col cols='12'>
          <div
            v-for='( task, i ) in tasks'
            :key='i'
          >

            <v-row class='task-row'>
              <!-- Task -->
              <v-col cols='10'>
                <Task :complete='task.completed' :name='task.name' />
              </v-col>

              <!-- Complete Button -->
              <v-col cols='1' class='text-center'>
                <v-btn :color='task.completed ? "info" : ""' fab small @click='toggleCompleted(i)'><v-icon>mdi-check</v-icon></v-btn>
              </v-col>

              <!-- Remove Button -->
              <v-col cols='1' class='text-center'>
                <v-btn color='error' fab small @click='removeTask(i)'><v-icon>mdi-close</v-icon></v-btn>
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
