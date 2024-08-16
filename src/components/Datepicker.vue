<template>
  <div>
    <VueDatePicker v-model="date"></VueDatePicker>
  </div>
</template>
<script>
import { ref } from 'vue';
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'

export default {
  name: 'Datepicker',
  components: {
    VueDatePicker
  },
  setup() {
    const date = ref();

    return {
      date
    }
  },
}
</script>
<style>
  
</style>