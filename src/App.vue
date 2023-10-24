<script setup>
import AppStyle from './assets/style/App.module.scss'
import Layout from "./components/Layout.vue";
import DefaultInput from './components/inputs/DefaultInput.vue';
import { reactive, ref, watch } from 'vue'
import PasswordInput from './components/inputs/passwordInput.vue'
import LimitedInput from './components/inputs/LimitedInput.vue'
import TextArea from './components/inputs/TextArea.vue'

// default input
const defaultInputValue = ref('')
const defaultResetTrigger = ref(0)
const defaultInputTips = reactive({
  success: '可以註冊使用',
  fail: '錯誤格式提示'
})
const defaultApproved = ref(true)
function setDefaultInputValue(data){
  defaultInputValue.value = data
}
// 驗證input內容範例
watch(defaultInputValue, ()=>{
  const pattern = /^[0-9]+$/;
  let ifPass = pattern.test(defaultInputValue.value)
  defaultApproved.value = ifPass
})
// big default input
const bigDefaultInputValue = ref('')
const bigDefaultResetTrigger = ref(0)
const bigDefaultInputTips = reactive({
  success: '可以註冊使用',
  fail: '錯誤格式提示'
})
const bigDefaultApproved = ref(true)
function setBigDefaultInputValue(data){
  bigDefaultInputValue.value = data
}
// 驗證input內容範例
watch(bigDefaultInputValue, ()=>{
  const pattern = /^[0-9]+$/;
  let ifPass = pattern.test(bigDefaultInputValue.value)
  bigDefaultApproved.value = ifPass
})

// password input
const passWordValue = ref('');
const resetPasswordTrigger = ref(0)
function setPassWordValue(data){
  passWordValue.value = data
}


</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" :class="AppStyle.logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" :class="[AppStyle.logo, AppStyle.vue]" alt="Vue logo" />
    </a>
    <h1>Vue+Vite+Element Plus Component Library</h1>
  </div>
  <el-row :gutter="20">
    <el-col :span="24">
      <h2>Input</h2>
    </el-col>
      <Layout>
        <DefaultInput
          @set-input-value="setDefaultInputValue"
          :title="'標題'"
          :placeholder="'請輸入關鍵字'"
          :approved="defaultApproved"
          :disabled="false"
          :tips="defaultInputTips"
          :resetTrigger="defaultResetTrigger"
          :initValue="'測試初始值'"
        ></DefaultInput>
      </Layout>
      <Layout>
        <DefaultInput
          @set-input-value="setBigDefaultInputValue"
          :title="'標題'"
          :placeholder="'請輸入關鍵字'"
          :approved="bigDefaultApproved"
          :disabled="false"
          :tips="bigDefaultInputTips"
          :resetTrigger="bigDefaultResetTrigger"
          :customStyle="'height:48px;font-size:16px;'"
        ></DefaultInput>
      </Layout>
      <Layout>
        <PasswordInput
          @set-input-value="setPassWordValue"
          :title="'設定密碼'"
          :placeholder="'使用8~20個英數混合字元'"
          :approved="true"
          :disabled="disabled"
          :tips="''"
          :resetTrigger="resetPasswordTrigger"
          :type="'password'"
          :show-password="true"
        ></PasswordInput>
      </Layout>
      <Layout>
        <PasswordInput
          @set-input-value="setPassWordValue"
          :title="'設定密碼'"
          :placeholder="'使用8~20個英數混合字元'"
          :approved="true"
          :disabled="disabled"
          :tips="''"
          :resetTrigger="resetPasswordTrigger"
          :type="'password'"
          :show-password="true"
          :customStyle="'height:48px;font-size:16px;'"
        ></PasswordInput>
      </Layout>
      <Layout>
        <LimitedInput
          @set-input-value="setPassWordValue"
          :title="'標題'"
          :placeholder="'請輸入關鍵字'"
          :approved="true"
          :disabled="disabled"
          :tips="''"
          :resetTrigger="resetPasswordTrigger"
          :type="'text'"
          :show-password="false"
          :maxlength="20"
          :show-word-limit="true"
        ></LimitedInput>
      </Layout>
      <Layout>
        <LimitedInput
          @set-input-value="setPassWordValue"
          :title="'標題'"
          :placeholder="'請輸入關鍵字'"
          :approved="true"
          :disabled="disabled"
          :tips="''"
          :resetTrigger="resetPasswordTrigger"
          :type="'text'"
          :show-password="false"
          :maxlength="20"
          :show-word-limit="true"
          :customStyle="'height:48px;font-size:16px;'"
        ></LimitedInput>
      </Layout>

  </el-row>
  <hr>
  <el-row :gutter="20">
    <el-col :span="24">
      <h2>Textarea</h2>
    </el-col>
    <Layout>
      <TextArea
          @set-input-value="setPassWordValue"
          :title="'標題'"
          :placeholder="'請輸入關鍵字'"
          :approved="true"
          :disabled="disabled"
          :tips="''"
          :resetTrigger="resetPasswordTrigger"
          :type="'textarea'"
          :show-password="false"
          :maxlength="20"
          :show-word-limit="true"
      ></TextArea>
    </Layout>
  </el-row>
</template>
<style>
body {
  background: #fff;
  color: #1F2937;
}
</style>
