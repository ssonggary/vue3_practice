<template>
  <div class="modal-wrap">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title fs-5">
            <slot name="title"></slot>
          </h5>
          <button 
            type="button" 
            class="btn-close"
            @click="onClose" 
            >
              &times;
            </button>
        </div>
        <div class="modal-body">
          <slot name="body"></slot>
        </div>
        <div class="modal-footer">
          <slot name="footer"></slot>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  setup(props, { emit }) {
    const onClose = () => {
      emit('close');
    }

    return {
      onClose,
    }
  }
}
</script>
<style scoped>
  .modal-wrap {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 10;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.3);
  }
</style>