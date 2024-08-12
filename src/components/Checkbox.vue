<template>
  <label 
  :for="id"
  :class="{'checked': modelValue, 'disabled': disabled}"
  class="checkbox"
  >
    <input
    :id="id"
    :checked="modelValue"
    :disabled="disabled"
    @change="handleChange"
    type="checkbox"
    class="checkbox__input"
    >
    <span class="checkbox__label"><slot></slot></span>
    <span class="checkbox__box"></span>
  </label>
</template>
<script>

export default {
  name: 'Checkbox',
  props: {
    id: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    modelValue: {
      type: Boolean,
      default: false
    },
  },
  setup(props, { emit }) {
    const {id, disabled, modalValue} = props;

    const handleChange = (e) => {
      emit('update:modelValue', e.target.checked);
    }

    return {
      handleChange
    }
  },
}
</script>
<style>
  
</style>