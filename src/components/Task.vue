<script>
export default {
  name: 'Task',
  props: [ 'name' ]
}
</script>

<template>
  <div class='task'>
    <v-card class='task-card'>{{  }}</v-card>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.task .task-card {
  padding: 12px;
}
</style>
