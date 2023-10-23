<template>
    <div>
        <el-input
        class="w-50 m-2"
        size="large"
        placeholder="Please Input"
        v-model="modelValue"
        />
    </div>
</template>
<script setup>
import { ref, defineEmits, watchEffect } from 'vue'

const modelValue = ref('')

const emitModelValue = defineEmits(['modelValue'])

watchEffect(() => {
    emitModelValue('setInputValue', modelValue.value)

})



</script>