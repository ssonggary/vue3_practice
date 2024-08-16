<template>
  <div 
    class="custom-input"
    :class="{ 'error': errorMessage }"
  >
    <label 
      :for="inputId"
      v-if="showLabel"
      class="custom-input__label"
      :class="{ 'bilnd': !showLabel}"
    >
      {{ label }}
    </label>
    <div class="custom-input__wrapper">
      <input 
        type="type"
        :id="inputId"
        :value="modelValue"
        :placeholder="placeholder"
        @input="updateValue"
        @blur="validateInput"
        class="custom-input__input"
      >
      <button 
        type="button"
        v-if="modelValue"
        @click="clearInput"
        class="custom-input__clear-btn"
      >
        x
      </button>
    </div>
    <p 
      v-if="errorMessage"
      class="custom-input__error-message"
    >
      {{ errorMessage }}
    </p>
  </div>
</template>
<script>
export default {
  name: 'CustomInput',
  props: {
    modelValue: String,
    type: {
      type: String,
      default: 'text',
    },
    validate: Function,
    placeholder: {
      type: String,
      default: "",
    },
    label: {
      type: String,
      default: "",
    },
    showLabel: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      errorMessage: "",
      inputId: `input-${Math.random().toString(36).substr(2,9)}`,
    }
  },
  methods: {
    updateValue(event) {
      this.$emit("update:modelValue", event.target.value);
      this.errorMessage = "";
    },
    clearInput() {
      this.$emit("update:modelValue", "");
      this.errorMessage = "";
    },
    validateInput() {
      if(this.validate) {
        this.errorMessage = this.validate(this.modelValue);
      }
    }
  },
}
</script>
<style>
  
</style>