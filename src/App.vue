<template>
  <v-app style='background-color: #EAEAEA'>
    <h1 id='title' class='text-center text-uppercase'>To Do List</h1>
    <v-main>
      <List />
    </v-main>
  </v-app>
</template>

<script>
import List from '@/components/List';

export default {
  name: 'App',
  components: { List },
  data: () => ({}),
};
</script>

<style scoped>
#title {
  color: #FFFFFF;
  border-radius: 0;
  padding: 16px 0;
  margin-bottom: 16px;
  border-bottom: 2px solid #00EEFF;
  background-color: #3F3F3F;
  box-shadow: 5px 5px 5px#DADADA;
}
</style>
