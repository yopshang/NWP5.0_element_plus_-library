<script setup>
import AppStyle from './assets/style/App.module.scss'
import Layout from "./components/Layout.vue";
import DefaultInput from './components/inputs/DefaultInput.vue';
import { ref } from 'vue'

const defaultInputValue = ref('')
function setDefaultInputValue(data){
  defaultInputValue.value = data
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
          :approved="true"
          :disabled="false"
          :tips="{
            success: '可以註冊使用',
            fail: '錯誤格式提示'
          }"
        ></DefaultInput>
      </Layout>
      <Layout>
          <el-button>Default</el-button>
          <el-button type="primary">Primary</el-button>
          <el-button type="success">Success</el-button>
          <el-button type="info">Info</el-button>
          <el-button type="warning">Warning</el-button>
          <el-button type="danger">Danger</el-button>
      </Layout>
      <Layout>
          <el-button>Default</el-button>
          <el-button type="primary">Primary</el-button>
          <el-button type="success">Success</el-button>
          <el-button type="info">Info</el-button>
          <el-button type="warning">Warning</el-button>
          <el-button type="danger">Danger</el-button>
      </Layout>
      <Layout>
          <el-button>Default</el-button>
          <el-button type="primary">Primary</el-button>
          <el-button type="success">Success</el-button>
          <el-button type="info">Info</el-button>
          <el-button type="warning">Warning</el-button>
          <el-button type="danger">Danger</el-button>
      </Layout>
      <Layout>
          <el-button>Default</el-button>
          <el-button type="primary">Primary</el-button>
          <el-button type="success">Success</el-button>
          <el-button type="info">Info</el-button>
          <el-button type="warning">Warning</el-button>
          <el-button type="danger">Danger</el-button>
      </Layout>
      <Layout>
          <el-button>Default</el-button>
          <el-button type="primary">Primary</el-button>
          <el-button type="success">Success</el-button>
          <el-button type="info">Info</el-button>
          <el-button type="warning">Warning</el-button>
          <el-button type="danger">Danger</el-button>
      </Layout>

  </el-row>
</template>
<style scope>
body {
  background: #fff;
  color: #1F2937;
}
</style>
