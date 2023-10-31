<template>
    <div :class="TextAreaStyle.TextAreaContainer">
        <div :class="DefaultInputStyle.title">{{ title }}</div>
        <el-input
            class="w-50 m-2"
            size="large"
            v-model="modelValue"
            :class="[checkInputStatus, customClass]"
            :style="customStyle"
            :placeholder="placeholder"
            :disabled="disabled"
            type="textarea"
            :show-password="showPassword"
            :maxlength="maxlength"
            :show-word-limit="showWordLimit"
            :custom-ref="customRef"
            @focus="userInputEvent('focus');ifFirstFocus = false"
            @blur="userInputEvent('blur')"
            @mouseover="changeStatusTo('hover')"
            @mouseleave="changeStatusTo('blur')"
            @keypress="userInputEvent('keypress')"
        />
        <div v-if="approved" :class="[DefaultInputStyle.tips,DefaultInputStyle['tips--success']]">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M9.00063 16.1703L5.53063 12.7003C5.14063 12.3103 4.51063 12.3103 4.12062 12.7003C3.73063 13.0903 3.73063 13.7203 4.12062 14.1103L8.30063 18.2903C8.69063 18.6803 9.32063 18.6803 9.71063 18.2903L20.2906 7.71031C20.6806 7.32031 20.6806 6.69031 20.2906 6.30031C19.9006 5.91031 19.2706 5.91031 18.8806 6.30031L9.00063 16.1703Z" fill="#65A30D"/>
            </svg>
            {{ tips.success }}
        </div>
        <div v-else :class="[DefaultInputStyle.tips,DefaultInputStyle['tips--fail']]">
            <svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg"> 
            <path d="M13.3007 0.709727C12.9107 0.319727 12.2807 0.319727 11.8907 0.709727L7.0007 5.58973L2.1107 0.699727C1.7207 0.309727 1.0907 0.309727 0.700703 0.699727C0.310703 1.08973 0.310703 1.71973 0.700703 2.10973L5.5907 6.99973L0.700703 11.8897C0.310703 12.2797 0.310703 12.9097 0.700703 13.2997C1.0907 13.6897 1.7207 13.6897 2.1107 13.2997L7.0007 8.40973L11.8907 13.2997C12.2807 13.6897 12.9107 13.6897 13.3007 13.2997C13.6907 12.9097 13.6907 12.2797 13.3007 11.8897L8.4107 6.99973L13.3007 2.10973C13.6807 1.72973 13.6807 1.08973 13.3007 0.709727Z" fill="#DC2626"/>
            </svg>
            {{ tips.fail }}
        </div>
    </div>
</template>
<style lang="scss">
@import '../../assets/style/variable.scss';
    .textArea {
        // .el-input__suffix {
        //     transform: translate(14px, 32px);
        // }
        &.hover:not(.error) .el-textarea__inner{
            box-shadow: 0 0 0 1px $default-input-outline-color--hover;
        }
        &.focus .el-textarea__inner{
            border:1px $default-input-outline-color--hover solid;
            box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.2);
        }
        &.default:not(.error) .el-textarea__inner{
            box-shadow: 0 0 0 1px $default-input-outline-color;
        }
        &.error .el-textarea__inner {
            box-shadow: 0 0 0 1px $default-input-outline-color--error !important;
        }
        .el-textarea__inner {
            height: 36px;
        }
        .el-textarea {
            margin-left: -20px;
        }
    }
</style>
<script setup>
import { ref, defineProps, defineEmits, watchEffect, watch, computed } from 'vue'
import DefaultInputStyle from '../../assets/style/components/DefaultInput.module.scss'
import TextAreaStyle from '../../assets/style/components/TextArea.module.scss';
import DefaultInput from './DefaultInput.vue';


const modelValue = ref('')
const checkInputStatus = ref('')
const showTips = ref(false)
const emitModelValue = defineEmits(['modelValue'])
// const approved_move_Y = ref(0)
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
    customRef: String
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

// const approved_move_Y = computed(()=>{
//     const textArea = this.$refs.TextArea.$refs.textarea; // 获取 TextArea 元素
//       const height = textArea.clientHeight; // 获取 TextArea 的高度
//       console.log('TextArea 的高度：', height);
//     return 0
// })

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
function handleResize(textAreaHeight){
    console.log('textAreaHeight:', textAreaHeight);
}



</script>