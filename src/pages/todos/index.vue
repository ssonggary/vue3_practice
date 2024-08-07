<template>
  <div>
    <div class="d-flex justify-content-between mb-3">
      <h2>To-Do List</h2>
      <button 
        type="button" 
        class="btn btn-primary"
        @click="moveToCreatePage"
      >
        새로운 할 일 만들기
      </button>
    </div>

    <input 
      class="form-control"
      type="text" 
      v-model="searchText"
      placeholder="검색어를 입력해 주세요."
    >
    <hr/>
    <div style="color: red"> {{ error }}</div>
    <div 
      v-if="!todos.length"
    >
      할 일이 없습니다.
    </div>
    <TodoList 
      :todos='todos' 
      @toggle-todo="toggleTodo" 
      @delete-todo="deleteTodo" 
    />
    <hr/>
    <nav aria-label="Page navigation example">
      <ul class="pagination">
        <li 
          class="page-item"
          v-if="currentPage !== 1"
        >
          <a class="page-link" style="cursor: pointer;" @click="getTodos(currentPage - 1)">Previous</a>
        </li>
        <li 
          class="page-item"
          v-for="page in numberOfPage"
          :key = "page"
          :class="currentPage === page ? 'active' : ''"
        >
          <a class="page-link" style="cursor: pointer;" @click="getTodos(page)">{{ page }}</a>
        </li>
        <li 
          class="page-item"
          v-if="numberOfPage !== currentPage"
        >
          <a class="page-link" style="cursor: pointer;" @click="getTodos(currentPage + 1)">Next</a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import { ref, computed, watch } from "vue";
import { useRouter } from 'vue-router';
import TodoList from '@/components/TodoList.vue';
import axios from '@/axios';

export default {
  components: {
    TodoList,
  },
  setup() {
    const router = useRouter();
    const todos = ref([]);
    const error = ref('');
    const numberOfTodos = ref(0);
    const limit = 5;
    const currentPage = ref(1);
    const searchText = ref('');

    const numberOfPage = computed(() => {
      return Math.ceil(numberOfTodos.value/limit);
    });
    
    const todoStyle = {
      textDecoration: 'line-through',
      color: 'gray' 
    }

    const getTodos = async (page = currentPage.value) => {
      currentPage.value = page;
      try {
        const res = await axios.get(
          `todos?_sort=id&_order=desc&subject_like=${searchText.value}&_page=${page}&_limit=${limit}`
        );
        numberOfTodos.value = res.headers['x-total-count'];
        todos.value = res.data;
      } catch (err) {
        console.log(err);
        triggerToast('문제가 생겼습니다!', 'danger');
      }
    }
    getTodos();

    const addTodo = async (todo) => {
      // 데이터베이스에 todo를 저장
      error.value = '';
      try {
        await axios.post('todos', {
          subject: todo.subject,
          complected: todo.complected,
        });
        getTodos(1);
      } catch (err) {
        console.log(err);
        triggerToast('문제가 생겼습니다!', 'danger');
      }
    };

    const toggleTodo = async (index, checked) => {
      error.value = '';
      const id = todos.value[index].id;
      try{
        await axios.patch('todos/' + id,{
          complected: checked
        });
        todos.value[index].complected = checked;
      } catch (err) {
        console.log(err);
        triggerToast('문제가 생겼습니다!', 'danger');
      }
    }

    const deleteTodo = async (id) => {
      error.value = '';
    
      try{
        await axios.delete('todos/' + id,{});
        getTodos(1);
      } catch (err) {
        console.log(err);
        triggerToast('문제가 생겼습니다!', 'danger');
      }
    }

    let timeout = null;
    watch(searchText, () => {
      clearTimeout(timeout);
      timeout = setTimeout(() => {
        getTodos(1);
      }, 2000);
    });

    const moveToCreatePage = () => {
      router.push({
        name: 'TodoCreate',
      })
    }

    return{
      todos,
      addTodo,
      deleteTodo,
      toggleTodo,
      searchText,
      error,
      numberOfPage,
      currentPage,
      getTodos,
      moveToCreatePage,
    };
  }
}
</script>

<style>
  .todo{
    color: #ccc;
    text-decoration: line-through;
  }
</style>