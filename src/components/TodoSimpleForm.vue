<template>
  <form @submit.prevent="onSubmit">
    <div class="d-flex">
      <div class="flex-grow-1 mr-2">
        <input 
          class="form-control"
          type="text" 
          v-model="todo"
          placeholder="새로운 할 일을 적어주세요."
        >
      </div>
      <div>
        <button 
          class="btn btn-primary"
          type="submit"
        >
        Add
        </button>
      </div>
    </div>
    <div v-show="hasError" style="color: red">할 일을 적어주세요.</div>
  </form>
</template>
<script>
import { ref } from "vue";

export default {
  emits: ['add-todo'],
  setup(props, { emit }) {
    const todo = ref('');
    const hasError = ref(false);

    const onSubmit = () => {
      if(todo.value === ''){
        hasError.value = true;
      } else {
        emit('add-todo', {
          id: Date.now(),
          subject: todo.value,
          complected: false,
        })
        hasError.value = false;
        todo.value = '';
      }
    };

    return{
      todo,
      hasError,
      onSubmit
    }
  }
}
</script>
<style>
    
</style>