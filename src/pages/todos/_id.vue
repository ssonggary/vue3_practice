<template>
  <div>
    <h1>To-Do Page</h1>
    <TodoForm :editing="true" />
  </div>
</template>
<script>
import TodoForm from '@/components/TodoForm.vue';

export default {
  components: {
    TodoForm,
  },

}
</script>
<style>
  
</style>