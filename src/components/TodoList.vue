<template>
  <div>
    <!-- <div 
      class="card mt-2"
      v-for="(todo, index) in todos"
      :key = "todo.id"
    > -->
    <List
      :items="todos"
    >
      <template #default="{ item, index }">
        <div 
          class="card-body p-2 d-flex align-items-center"
          style="cursor: pointer;"
          @click="moveToPage(item.id)"
        >
          <div class="form-check flex-grow-1">
            <input
              class="form-check-input" 
              type="checkbox"
              :checked="item.complected"
              @change="toggleTodo(index, $event)"
              @click.stop
            >
            <label 
              class="form-check-label label"
              :class="{todo: item.complected}"
            >
              {{ item.subject }}
            </label>
          </div>
          <div>
            <button 
              class="btn btn-danger btn-sm" 
              type="button"
              @click.stop="opnetModal(item.id)"
              >
                Delete
            </button>
          </div>
        </div>
      </template>
    </List>
    <!-- </div> -->
    <Teleport to="body">
      <Modal 
        v-if="showModal"
        @close="closeModal"
        @delete ="deleteTodo"
      />
    </Teleport>
  </div>
</template>

<script>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import Modal from '@/components/DeleteModal.vue';
import List from '@/components/List.vue';

export default {
  components: {
    Modal,
    List,
  },
  props: {
    todos: {
      type: Array,
      required: true
    }
  },
  emits: ['toggle-todo', 'delete-todo'],
  setup(props, { emit }) {
    const router = useRouter();
    const showModal = ref(false);
    const todoDeleteId = ref(null);

    const opnetModal = (id) => {
      todoDeleteId.value = id;
      showModal.value = true;
    }

    const closeModal = () => {
      todoDeleteId.value = null;
      showModal.value = false;
    }

    const toggleTodo = (index, event) => {
      emit('toggle-todo', index, event.target.checked);
    }

    const deleteTodo = () => {
      emit('delete-todo', todoDeleteId.value);
      
      showModal.value = false;
      todoDeleteId.value = null;
    }

    const moveToPage = (todoId) => {
      // router.push('/todos/' + todoId);
      router.push({
        name: 'Todo',
        params: {
          id: todoId
        }
      });
    }

    return {
      toggleTodo,
      deleteTodo,
      moveToPage,
      showModal,
      opnetModal,
      closeModal,
    }
  }
}
</script>

<style>
  .label {
    cursor: pointer;
  }
</style>