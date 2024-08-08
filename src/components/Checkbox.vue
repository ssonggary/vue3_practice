<template>
  <label 
  :for="id"
  class="checkbox"
  >
    <input
    :id="id" 
    type="checkbox"
    class="checkbox__input"
    >
    <span class="checkbox__label"><slot></slot></span>
    <span class="checkbox__box"></span>
  </label>
</template>
<script>
export default {
  
}
</script>
<style>
  
</style>