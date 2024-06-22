<template>
  <div>
    <div class="input-container-1">
      <input type="text" v-model="formattedInputValue" @input="handleInput" placeholder="Enter number">
    </div>
    <div class="input-container-2">
      <input type="checkbox" v-model="inputCheck">
      <input type="text" :class="{'inputCheckTrue': inputCheck, 'inputCheckFalse': !inputCheck}" placeholder="Enter number">
    </div>
  </div>
</template>

<script>
export default {
  name:"InputComponent",
  data(){
    return{
      inputCheck: false,
      formattedInputValue : '',
    }
  },
  methods: {
    handleInput(e) {
      this.formattedInputValue = this.numberFormatThree(e.target.value)
    },
    numberFormatThree(value) {
      if (!value) return '';
      let formattedValue = value.replace(/\s/g, "");
      formattedValue = formattedValue.replace(/\B(?=(\d{3})+(?!\d))/g, " ");
      return formattedValue;
    }
  }
}
</script>

<style scoped>
.input-container-1 {
  position: relative;
  width: 300px;
}

.input-container-1 input {
  width: 100%;
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
  transition: border-color 0.3s, box-shadow 0.3s;
}

.input-container-1 input:focus {
  border-color: #007BFF;
  box-shadow: 0 0 8px rgba(0, 123, 255, 0.2);
  outline: none;
}
.input-container-2 {
  display: flex;
  align-items: center;
  gap: 30px;
  width: 300px;
  margin: 30px 0;
}
.inputCheckFalse{
  width: 100%;
  padding: 10px;
  border: 2px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}
.inputCheckTrue{
  width: 100%;
  padding: 10px;
  border-radius: 4px;
  font-size: 16px;
  border-color: #007BFF;
  color: #007BFF ;
  outline: none;
}
</style>