<script>
export default {
  name: 'Task',
  props: [ 'name', 'complete' ],
  computed: {
    getColor() {
      return this.complete && '#4C6673';
    }
  }
}
</script>

<template>
  <div class='task'>
    <v-card class='task-card' :color='getColor'>{{ name }}</v-card>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.task .task-card {
  padding: 12px;
}
</style>
