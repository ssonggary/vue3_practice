<template>
  <Modal>
    <template #title>
      할 일 삭제하기!!
    </template>
    <template #body>
      선택한 할 일을 지우시겠습니까?
    </template>
    <template #footer>
      <button 
        type="button" 
        class="btn btn-secondary"
        @click="onClose"
        >
        취소
      </button>
      <button 
        type="button" 
        class="btn btn-danger"
        @click="onDelete" 
        >
          삭제
      </button>
    </template>
  </Modal>
</template>
<script>
import Modal from '@/components/Modal.vue';

export default {
  components: {
    Modal
  },
  setup(props, { emit }) {
    const onClose = () => {
      emit('close');
    }

    const onDelete = () => {
      emit('delete');
    }

    return {
      onClose,
      onDelete
    }
  }
}
</script>
<style >
  
</style>