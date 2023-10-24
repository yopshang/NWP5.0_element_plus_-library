<template>
    <DefaultInput
        @set-input-value="setModelValue"
        :title="title"
        :placeholder="placeholder"
        :approved="approved"
        :disabled="disabled"
        :tips="tips"
        :resetTrigger="resetTrigger"
        :type="password"
        :show-password="true"
    ></DefaultInput>
</template>
<style scope lang="scss">
   
</style>
<script setup>
import { ref, defineProps, defineEmits, watchEffect, watch } from 'vue'
// import DefaultInputStyle from '../../assets/style/DefaultInput.module.scss'
import DefaultInput from './DefaultInput.vue';


const modelValue = ref('')
const checkInputStatus = ref('')
const showTips = ref(false)
const emitModelValue = defineEmits(['modelValue'])
const props = defineProps({
    title: String,
    placeholder: String,Number,
    approved: Boolean,
    disabled: Boolean,
    tips: Object,String,
    resetTrigger: Number,
    customStyle: String,
    suffixIcon: Object,
    prefixIcon:Object,
    disabled: Boolean
})
watchEffect(() => {
    emitModelValue('setInputValue', modelValue.value)
})
watch(()=>props.resetTrigger, ()=>{
    modelValue.value = ''
    changeStatusTo('blur')
    showTips.value = false;
})
watch()

function changeStatusTo(thisStatus){
    switch(thisStatus){
        case 'focus':
            checkInputStatus.value = 'focus';
            break;
        case 'blur':
            checkInputStatus.value = 'default';
            break;
        case 'hover':
            checkInputStatus.value = 'hover';
            break;
        case 'error':
            checkInputStatus.value = 'error';
            break;
        default:
            checkInputStatus.value = 'default';
            break;
    }
}
function userInputEvent(inputStatus){
    showTips.value = true;
    let changeStatusToThis = props.approved?inputStatus:'error';
    changeStatusTo(changeStatusToThis)
}
function setModelValue(data){
    modelValue.value = data
}



</script>