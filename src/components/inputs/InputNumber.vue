<template>
    <el-input-number
        v-model="num"
        class="InputNumber"
        :class="InputNumberStyle.defaultInputNumber"
        :min="1"
        :max="10"
        @change="handleChange" />
</template>

<script setup>
import { ref } from 'vue'
import InputNumberStyle from '../../assets/style/components/InputNumber.module.scss'

const num = ref(1)
const handleChange = (value) => {
    console.log(value)
}
</script>
<style lang="scss">
.InputNumber{

}
</style>