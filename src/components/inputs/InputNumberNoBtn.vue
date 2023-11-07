<template>
    <input
        v-model="num"
        class="InputNumberNobtn"
        :class="[InputNumberNoBtnStyle.InputNumberNoBtnStyle,checkInputStatus]"
        :min="1"
        :max="10"
        :disabled="disabled"
        @input="replaceNonNumeric"
        @change="handleChange"
        @focus="userInputEvent('focus');ifFirstFocus = false"
        @blur="userInputEvent('blur')"
        @mouseover="changeStatusTo('hover')"
        @mouseleave="changeStatusTo('blur')"
        @keypress="userInputEvent('keypress')" />
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'
// import InputNumberStyle from '../../assets/style/components/InputNumber.module.scss'
import InputNumberNoBtnStyle from '../../assets/style/components/InputNumberNoBtn.module.scss'

const num = ref(0)
const ifFirstFocus = ref(true)
const checkInputStatus = ref('default')
const setInputValue = defineEmits(['setInputValue'])
const handleChange = (value) => {
    setInputValue('setInputValue', value)
}
const props = defineProps({
    disabled: Boolean,
    initValue: Number,
    approved: Boolean
})
// 控制輸入框狀態
function changeStatusTo(thisStatus){
    if(!props.approved && !ifFirstFocus.value){ // 第一次 focus前不進行錯誤判定
        checkInputStatus.value = 'error';
        return
    }
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
// 控制有警示字樣的輸入框狀態
function userInputEvent(inputStatus){
    // if(props.tips == '') return
    // 轉為非同步避免樣式過早判定
    setTimeout(function(){
            changeStatusTo(inputStatus)
    },0)
}
// 替換掉非數字
function replaceNonNumeric() {
      num.value = num.value.replace(/\D/g, '');
    }
// 父層傳入的初始值
num.value = props.initValue;

</script>
<style lang="scss">
@import '../../assets/style/variable.scss';
.InputNumberNobtn{
    &.default {
        @extend .default-input-border;
    }
    &.focus{
        @extend .default-input-outline--focus;
        // border:solid 1px $default-input-outline-color--hover;
        // box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.2);
    }
    &.hover{
        @extend .default-input-border--hover;
        // border: solid 1px $default-input-outline-color--hover;
        outline: none;
    }
    &.error {
        box-shadow: 0 0 0 1px $default-input-outline-color--error !important;
    }
    &.is-disabled {
        background: $default-input-background-color--disabled !important;
    }
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
            -webkit-appearance: none;
            margin: 0;
    }

    input[type=number] {
        -moz-appearance: textfield;
    }

}
</style>