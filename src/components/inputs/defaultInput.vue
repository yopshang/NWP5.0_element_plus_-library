<template>
    <div :class="DefaultInputStyle.container">
        <div :class="DefaultInputStyle.title">{{ title }}</div>
        <el-input
        class="w-50 m-2"
        :class="[DefaultInputStyle.custom_input, checkInputStatus]"
        size="large"
        :placeholder="placeholder"
        :disabled="disabled"
        v-model="modelValue"
        @focus="changeStatusTo('focus')"
        @blur="changeStatusTo('blur')"
        @mouseover="changeStatusTo('hover')"
        @mouseleave="changeStatusTo('blur')"
        @keypress="changeStatusTo('blur')"
        />
    </div>
</template>
<style scope lang="scss">
    .hover{
        border:1px #3B82F6 solid;
    }
    .focus,
    .focus-visible {
        border:1px #3B82F6 solid;
        box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.2);
    }
    .default{
        border:1px #E5E7EB solid;
    }
    .is-disabled>.el-input__wrapper{
        background: #E5E7EB !important;
    }
</style>
<script setup>
import { ref, defineProps, defineEmits, watchEffect } from 'vue'
import DefaultInputStyle from '../../assets/style/DefaultInput.module.scss'

const modelValue = ref('')
const checkInputStatus = ref('')
const emitModelValue = defineEmits(['modelValue'])
watchEffect(() => {
    emitModelValue('setInputValue', modelValue.value)
})
const props = defineProps({
    title: String,
    placeholder: String,Number,
    approved: Boolean,
    disabled: Boolean
})

function changeStatusTo(thisStatus){
    if(thisStatus == 'focus'){
        console.log('focus')
        checkInputStatus.value = 'focus';
    } else if (thisStatus == 'blur'){
        console.log('blur')
        checkInputStatus.value = 'default';
    } else if( thisStatus == 'hover'){
        checkInputStatus.value = 'hover';
    } else {
        checkInputStatus.value = 'default';
    }
}



</script>