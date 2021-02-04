<script>
import Task from '@/components/Task'
import data from '@/mock-api.js'

export default {
  name: 'List',
  components: {},
  data: () => ({
    tasks: data.tasks,
    input: ''
  }),
  methods: {

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
          <v-btn>Add Task</v-btn>
        </v-col>

      <v-row>
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
                <Task />
              </v-col>

              <!-- Complete Button -->
              <v-col cols='2'>
                <v-btn>complete</v-btn>
              </v-col>

              <!-- Remove Button -->
              <v-col cols='2'>
                <v-btn>remove</v-btn>
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
