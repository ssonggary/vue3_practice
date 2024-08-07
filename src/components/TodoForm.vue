<template>
  <div>
    <div v-if="loading">
      Loding...
    </div>
    <form 
      v-else
      @submit.prevent="onSave"
    >
      <div class="row">
        <div class="col-6">
          <Input 
            label="Subject"
            v-model:subject="todo.subject"
            :error="subjectError"
          />
          <!-- <div class="form-group">
            <label>Subject</label>
            <input 
              type="text" 
              class="form-control"
              v-model="todo.subject"
            >
            <div v-if="subjectError" class="text-red">
              {{ subjectError }}
            </div>
          </div> -->
        </div>
        
        <div v-if="editing" class="col-6">
          <div class="form-group">
            <label>상태</label>
            <div>
              <button 
                type="button"
                class="btn"
                :class="todo.complected ? 'btn-success' : 'btn-danger'"
                @click="toggleTodoStatus"
              >
                {{ todo.complected ? '완료' : '미완료' }}
              </button>
            </div>
          </div>
        </div>
        <div class="col-12">
          <div class="form-group">
            <label>메모</label>
            <textarea v-model="todo.body" class="form-control" name="" id="" cols="30" rows="10"></textarea>
          </div>
        </div>
      </div>
      
      <button 
        type="submit" 
        class="btn btn-primary"
        :disabled="!todoUpdated"
        >
        {{ editing ? '수정' : '만들기' }}
      </button>
      <button 
        type="button" 
        class="btn btn-outline-secondary ml-2"
        @click="moveToTodoList"
        >
        취소
      </button>
    </form>
  </div>
</template>
<script>
import { ref, computed} from 'vue';
import axios from '@/axios';
import { useRoute, useRouter } from 'vue-router';
import _ from 'lodash';
import { useToast } from '@/composables/toast';
import Input from '@/components/Input.vue'

export default {
  components: {
    Input,
  },
  props: {
    editing: {
      type: Boolean,
      default: false
    }
  },
  setup(props) {
    const route = useRoute();
    const router = useRouter();
    const todo = ref({
      subject: '',
      complected: false,
      body: ''
    });
    const origianlTodo = ref(null);
    const loading = ref(false);
    const todoId = route.params.id;
    const subjectError = ref('');

    const {
      triggerToast,
    } = useToast();


    const getTodo = async () => {
      loading.value = true;
      try{
        const res = await axios.get(`todos/${todoId}`);
        
        todo.value = {...res.data};
        origianlTodo.value = {...res.data};

        loading.value = false;
      } catch (error) {
        console.log(error);
        loading.value = false;
        triggerToast('문제가 생겼습니다!', 'danger');
      }
    }

    const todoUpdated = computed(() => {
      return !_.isEqual(todo.value, origianlTodo.value)
    })

    const toggleTodoStatus = () => {
      todo.value.complected = !todo.value.complected;
    }

    if(props.editing){
      getTodo();
    }


    const moveToTodoList = () => {
      router.push({
        name: 'Todos',
      })
    }

    const onSave = async () => {
      subjectError.value = '';
      if(!todo.value.subject) {
        subjectError.value = '제목을 작성해 주세요.';
        return;
      }

      try{
        let res;
        const data = {
          subject: todo.value.subject,
          complected: todo.value.complected,
          body: todo.value.body,
        }
        if(props.editing){
          res = await axios.put(`todos/${todoId}`, data);
          origianlTodo.value = {...res.data}
        } else {
          res = await axios.post('todos', data);
          todo.value.subject = '';
          todo.value.body = '';
        }

        const message = (props.editing ? '업데이트가 완료되었습니다!' : '저장을 완료했습니다!')
        triggerToast(message);

        if(!props.editing) {
          router.push({
            name: 'Todos'
          });
        }
      } catch(error) {
        console.log(error);
        triggerToast('문제가 생겼습니다!', 'danger');
      }
    }

    return{
      todo,
      loading,
      toggleTodoStatus,
      moveToTodoList,
      onSave,
      todoUpdated,
      subjectError,
    }
  }
}
</script>
<style>
  
</style>