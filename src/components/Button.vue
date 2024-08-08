<template>
  <button 
  type="button"
  :class="['btn', variantClass]"
  :disabled="disabled"
  @click="handleClick"
  >
    <i 
    v-if="icon"
    :class="iconClass"
    class="btn__icon"
    ></i>
    <span class="btn__text"><slot></slot></span>
  </button>
</template>
<script>
import { computed} from 'vue';

export default {
  name: 'Button',
  props: {
    variant: {
      type: String,
      default: 'default',
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false
    },
    icon: {
      type: String,
      default: ''
    },
  },

  setup(props) {
    const {variant, disabled, icon} = props;

    const handleClick = (e) => {
      console.log('asdasdasd');
    };

    const variantClass = computed(() => {
      return `btn--${variant}`
    })
    const iconClass = computed(() => {
      return `icon-${icon}`
    })

    return {
      variantClass,
      handleClick,
      iconClass
    }
  },
}
</script>
<style scoped>
  
</style>