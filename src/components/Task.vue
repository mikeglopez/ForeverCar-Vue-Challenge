<script>
export default {
  name: 'Task',
  props: [ 'name', 'complete' ],
  computed: {
    getClass() {
      return this.complete && 'text-decoration-line-through blue-grey--text text--lighten-3'
    }
  }
}
</script>

<template>
  <div class='task'>
    <v-card class='task-card' :class='getClass'>{{ name }}</v-card>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.task .task-card {
  padding: 12px;
}
</style>
