<template>
    <DefaultInput
        @set-input-value="setModelValue"
        :title="title"
        :placeholder="placeholder"
        :approved="approved"
        :disabled="disabled"
        :tips="''"
        :resetTrigger="resetTrigger"
        type="textarea"
        :show-password="true"
        :customStyle="customStyle"
        :maxlength="maxlength"
        :show-word-limit="true"
        :custom-class="'textArea'"
    ></DefaultInput>
    <!-- <div v-if="tips != ''"> -->
    <div>
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
</template>
<style lang="scss">
    .textArea {
        .el-input__suffix {
            transform: translate(14px, 32px);
        }
        .el-textarea__inner:focus {
            // box-shadow: 0 0 0 1px #3B82F6;
            border:1px #3B82F6 solid;
            box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.2);
        }
    }
</style>
<script setup>
import { ref, defineProps, defineEmits, watchEffect, watch } from 'vue'
import DefaultInputStyle from '../../assets/style/DefaultInput.module.scss'
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
    disabled: Boolean,
    customStyle: String,
    maxlength: Number,Boolean,
    customClass: String,
    initValue: String,Number, // 傳入初始值
    beforeSubmitVerificationTrigger: Number, // 強制出現驗證樣式（直接送出前呼叫）
})
watchEffect(() => {
    emitModelValue('setInputValue', modelValue.value)
})
watch(()=>props.resetTrigger, ()=>{
    modelValue.value = ''
    changeStatusTo('blur')
    showTips.value = false;
})
watch(()=>props.approved,()=>{
    console.log('textArea props.type:',props.type)
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
// function userInputEvent(inputStatus){
//     showTips.value = true;
//     let changeStatusToThis = props.approved?inputStatus:'error';
//     changeStatusTo(changeStatusToThis)
// }
function setModelValue(data){
    modelValue.value = data
}



</script>