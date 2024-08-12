<template>
  <div>
    Home page
    <ButtonGroup>
      <Button>접수</Button>
      <Button disabled>취소</Button>
    </ButtonGroup>
    <hr>
    <Button variant="line">신규</Button>
    <Button icon="delete" variant="line">삭제</Button>
    <Button icon="link">CHECK</Button>
    <hr>
    <Checkbox id="checkbox1" v-model="isChecked1">체키라웃췍췍</Checkbox>
    <Checkbox id="checkbox3" v-model="isChecked3">체키라웃췍췍22</Checkbox>
    <Checkbox id="checkbox2" v-model="isChecked2" disabled>체키라웃췍췍</Checkbox>
  </div>
</template>
<script>
import Button from '@/components/Button.vue';
import ButtonGroup from '@/components/ButtonGroup.vue';
import Checkbox from '@/components/Checkbox.vue';

export default {
  components: {
    Button,
    ButtonGroup,
    Checkbox
  },
  data() {
    return {
      isChecked1: false,
      isChecked2: false,
      isChecked3: false,
    }
  },
}
</script>
<style >
  
</style>