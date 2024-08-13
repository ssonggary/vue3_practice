<template>
  <div class="radio-group">
    <Radio
      v-for="option in options"
      :key="option.value"
      v-model="selectValue"
      :name="name"
      :value="option.value"
      :id="option.id"
      :disabled="option.disabled"
    >
      {{ option.label }}
    </Radio>
  </div>
</template>
<script>
import Radio from './Radio.vue';
export default {
  name: 'RadioGroup',
  components: {
    Radio
  },
  props: {
    options: {
      type: Array,
      required: true,
      default: () => []
    },
    modelValue: {
      type: [String, Number, Boolean],
      required: true,
    },
    name: {
      type: String,
      required: true,
    }
  },
  computed: {
    selectValue: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit('update:modelValue', value);
      }
    }
  }
}
</script>
<style>
  
</style>