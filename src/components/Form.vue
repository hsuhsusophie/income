<template>
    <form  @submit.prevent="FormHandler">
      <input type="text" placeholder="收入名稱" v-model="formData.desc" />
      <input type="number" placeholder="金額" v-model="formData.value" />
      <input type="date" placeholder="Income Date..." v-model="formData.date" />
      <input type="submit" value="提交" />
    </form>
  </template>
  
  <script>
  import { reactive } from 'vue';
  export default {
    props: {
      state: Object
    },
    setup (props, { emit }) {
      const formData = reactive({
        desc: null,
        value: null,
        date: null
      });
      function FormHandler () {
        emit("add-income", {
          desc: formData.desc,
          value: formData.value,
          date: formData.date
        });
        
        formData.desc = null;
        formData.value = null;
        formData.date = null;
      }
      // Return template data
      return {
        FormHandler,
        formData
      }
    }
  }
  </script>
  
  <style scoped>
    form {
      display: flex;
      justify-content: center;
      margin-top: 30px;
      margin-left: 10px;
      margin-right: 10px;
    }
    form input {
      color: #888;
      border: none;
      outline: none;
      font-size: 20px;
      width: 160px;
    }
    form input::placeholder {
      color: #AAA;
      font-size: 150;
    }
    form input:not([type="submit"]) {
      display: block;
      background: #FFF;
      border: none;
      outline: none;
      padding: 5px 15px;
    }
    form input[type="submit"] {
      display: block;
      background: none;
      border: none;
      outline: none;
      color: #FFF;
      font-weight: 400;
      text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
      padding: 5px 15px;
      background-color:  #787878;
      cursor: pointer;
    }
    form input:first-of-type {
      border-radius: 8px 0px 0px 8px;
    }
    form input:last-of-type {
      border-radius: 0px 8px 8px 0px;
    }

    @media screen and (max-width: 768px) {
      form {
      display: flex;
      justify-content: center;
      margin-top: 30px;
      max-width: 100%;    }
  
    }
  </style>