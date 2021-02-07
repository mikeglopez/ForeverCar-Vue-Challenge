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
      this.tasks.push({ name: this.input });
    },
    removeTask(task) {
      this.tasks.splice(task, 1);
    },
    toggleCompleted(index) {
      let task = this.tasks[index];
      if (task.completed) {
        task.completed = !task.completed;
      } else {
        task.completed = true;
      }

      this.$set(this.tasks, index, task);
    }
  }
}
</script>

<template>
  <v-form>
    <v-container>
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
        <v-col cols='2'>
          <v-btn @click='addTask'>Add Task</v-btn>
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
              <v-col cols='8'>
                <Task :complete='task.completed' :name='task.name' />
              </v-col>

              <!-- Complete Button -->
              <v-col cols='2'>
                <v-btn @click='toggleCompleted(i)'>complete</v-btn>
              </v-col>

              <!-- Remove Button -->
              <v-col cols='2'>
                <v-btn @click='removeTask(i)'>remove</v-btn>
              </v-col>
            </v-row>

          </div>
        </v-col>

      </v-row>
    </v-container>
  </v-form>
</template>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
.task-row {
  margin: 20px 0;
}
</style>
