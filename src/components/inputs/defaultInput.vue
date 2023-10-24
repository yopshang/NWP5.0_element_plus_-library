<template>
    <div :class="DefaultInputStyle.container" class="defaultInput">
        <div :class="DefaultInputStyle.title">{{ title }}</div>
        <el-input
        class="w-50 m-2"
        :class="[DefaultInputStyle.custom_input, checkInputStatus, customClass]"
        :style="customStyle"
        size="large"
        :placeholder="placeholder"
        :disabled="disabled"
        :type="type"
        :show-password="showPassword"
        :maxlength="maxlength"
        :show-word-limit="showWordLimit"
        v-model="modelValue"
        @focus="userInputEvent('focus')"
        @blur="userInputEvent('blur')"
        @mouseover="changeStatusTo('hover')"
        @mouseleave="changeStatusTo('blur')"
        @keypress="userInputEvent('keypress')"
        />
        <div v-if="tips != ''">
            <div v-if="approved && showTips" :class="[DefaultInputStyle.tips,DefaultInputStyle['tips--success']]">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M9.00063 16.1703L5.53063 12.7003C5.14063 12.3103 4.51063 12.3103 4.12062 12.7003C3.73063 13.0903 3.73063 13.7203 4.12062 14.1103L8.30063 18.2903C8.69063 18.6803 9.32063 18.6803 9.71063 18.2903L20.2906 7.71031C20.6806 7.32031 20.6806 6.69031 20.2906 6.30031C19.9006 5.91031 19.2706 5.91031 18.8806 6.30031L9.00063 16.1703Z" fill="#65A30D"/>
                </svg>
                {{ tips.success }}
            </div>
            <div v-else-if="showTips" :class="[DefaultInputStyle.tips,DefaultInputStyle['tips--fail']]">
                <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg"> 
                <path d="M13.3007 0.709727C12.9107 0.319727 12.2807 0.319727 11.8907 0.709727L7.0007 5.58973L2.1107 0.699727C1.7207 0.309727 1.0907 0.309727 0.700703 0.699727C0.310703 1.08973 0.310703 1.71973 0.700703 2.10973L5.5907 6.99973L0.700703 11.8897C0.310703 12.2797 0.310703 12.9097 0.700703 13.2997C1.0907 13.6897 1.7207 13.6897 2.1107 13.2997L7.0007 8.40973L11.8907 13.2997C12.2807 13.6897 12.9107 13.6897 13.3007 13.2997C13.6907 12.9097 13.6907 12.2797 13.3007 11.8897L8.4107 6.99973L13.3007 2.10973C13.6807 1.72973 13.6807 1.08973 13.3007 0.709727Z" fill="#DC2626"/>
                </svg>
    
                {{ tips.fail }}
            </div>
        </div>
    </div>
</template>
<style lang="scss">
.defaultInput {
    .hover:not(.textArea) .el-input__wrapper{
        // border:1px #3B82F6 solid;
        box-shadow: 0 0 0 1px #3B82F6;
    }
    .focus,
    .focus-visible{
        border:1px #3B82F6 solid;
        box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.2);
    }
    .default:not(.error) .el-input__wrapper{
        // border:1px #E5E7EB solid;
        box-shadow: 0 0 0 1px #E5E7EB;
    }
    .error {
        // box-shadow: 0 0 0 1px #DC2626;
        // border:1px #DC2626 solid;
        .el-input__wrapper {
            box-shadow: 0 0 0 1px #DC2626 !important;
        }
    }
    .is-disabled>.el-input__wrapper{
        background: #E5E7EB !important;
    }
    .el-input__wrapper {
        box-shadow: none !important;
    }
}
</style>
<script setup>
import { ref, defineProps, defineEmits, watchEffect, watch } from 'vue'
import DefaultInputStyle from '../../assets/style/DefaultInput.module.scss'

const modelValue = ref('')
const checkInputStatus = ref('')
const showTips = ref(false)
const emitModelValue = defineEmits(['modelValue'])
const props = defineProps({
    title: String,
    placeholder: String,Number,
    approved: Boolean,
    disabled: Boolean,
    tips: Object,
    resetTrigger: Number,
    customStyle: String,
    suffixIcon: Object,
    prefixIcon:Object,
    type: String,
    showPassword: Boolean,
    showWordLimit: Boolean,
    maxlength: Number,
    customClass: String,
    initValue: String,Number,
})
watchEffect(() => {
    emitModelValue('setInputValue', modelValue.value)
})
watch(()=>props.resetTrigger, ()=>{
    modelValue.value = ''
    changeStatusTo('blur')
    showTips.value = false;
})

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
    // 轉為非同步避免樣式過早判定
    setTimeout(function(){
        showTips.value = true;
        let changeStatusToThis = props.approved?inputStatus:'error';
        changeStatusTo(changeStatusToThis)
    },0)
}
modelValue.value = props.initValue;




</script>