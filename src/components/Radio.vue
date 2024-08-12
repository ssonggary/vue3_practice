<template>
  <label
  class="radio" 
  :class="{'checked': modelValue === value, 'disabled': disabled}"
  :form="id"
  
  >
    <input 
      type="radio"
      :id="id"
      :checked="modelValue === value"
      :disabled="disabled"
      :name="name"
      :value="value"
      @change="handleChange"
      class="radio__input"
    >
    <span class="radio__label"><slot></slot></span>
    <span class="radio__circle"></span>
  </label>
</template>
<script>
export default {
  name: 'Radio',
  props: {
    modelValue: {
      type:[String, Number, Boolean],
      requied: true,
    },
    value: {
      type: [String, Number, Boolean],
      requied: true,
    },
    id: {
      type: String,
      requied: true,
    },
    name: {
      type: String,
      requied: true,
    },
    disabled: {
      type: Boolean,
      default: false
    },
  },
  setup(props, { emit }) {

    const handleChange = (e) => {
      emit('update:modelValue', props.value);
    }

    return {
      handleChange
    }
  },
}
</script>
<style>
  
</style>