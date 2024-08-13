<template>
  <div>
    컴포넌트 만들어보기
    <hr>
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
    <hr>
    <Radio 
      name="radioGroup1" 
      id="radio1"
      value="option1"
      v-model="selectedOption"
    >
      라디오버튼 1
    </Radio>
    <Radio 
      name="radioGroup1" 
      id="radio2"
      value="option2"
      v-model="selectedOption"
    >
      라디오버튼 2
    </Radio>
    <Radio 
      name="radioGroup1" 
      id="radio3"
      value="option3"
      disabled
      v-model="selectedOption"
    >
      라디오버튼 3
    </Radio>
    <hr>
    <RadioGroup 
      v-model="selectedRadioOption"
      name="radioGroup2"
      :options="radioOptions"
    ></RadioGroup>
    <hr>
    <CustomInput
      v-model="inputValue"
      :validate="validateInput"
      label="DEFAULT"
      placeholder="TXT"
    ></CustomInput>
    <CustomInput
      v-model="inputValue"
      :validate="validateInput"
      label="블라인드 라벨"
      placeholder="TXT"
      :showLabel ='false'
    ></CustomInput>
  </div>
</template>
<script>
import Button from '@/components/Button.vue';
import ButtonGroup from '@/components/ButtonGroup.vue';
import Checkbox from '@/components/Checkbox.vue';
import Radio from "@/components/Radio.vue";
import RadioGroup from '@/components/RadioGroup.vue';
import CustomInput from '@/components/CustomInput.vue';

export default {
  components: {
    Button,
    ButtonGroup,
    Checkbox,
    Radio,
    RadioGroup,
    CustomInput,
  },
  data() {
    return {
      // checkbox
      isChecked1: false,
      isChecked2: false,
      isChecked3: false,
      // radio
      selectedOption: 'option1',
      // radioGroup
      selectedRadioOption: '',
      radioOptions: [
        {label: '라디오그룹1', value: 'op1', id: 'radio1', disabled: false},
        {label: '라디오그룹2', value: 'op2', id: 'radio2', disabled: false},
        {label: '라디오그룹3', value: 'op3', id: 'radio3', disabled: false},
        {label: '라디오그룹4', value: 'op4', id: 'radio4', disabled: false}
      ],
      // input
      inputValue: "",
    }
  },
  methods: {
    validateInput(value) {
      if(!value) {
        return "THIS IS AN ERROR MASSEGE.";
      } else if (value.length < 5) {
        return "5글자 이상 작성해주세요."
      } return "";
    }
  }
}
</script>
<style >
  
</style>