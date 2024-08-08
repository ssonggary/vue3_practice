<template>
  <div>
    Home page
    <Button>접수</Button>
    <Button disabled>취소</Button>
    <Button variant="line">신규</Button>
    <Button icon="delete" variant="line">삭제</Button>
    <Button icon="link">CHECK</Button>
  </div>
</template>
<script>
import Button from '@/components/Button.vue';

export default {
  components: {
    Button,
  },
}
</script>
<style >
  
</style>