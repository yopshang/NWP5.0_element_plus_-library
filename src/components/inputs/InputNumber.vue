<template>
    <el-input-number
        v-model="num"
        class="InputNumber"
        :class="[InputNumberStyle.defaultInputNumber,checkInputStatus]"
        :min="1"
        :max="10"
        :disabled="disabled"
        @change="handleChange"
        @focus="userInputEvent('focus');ifFirstFocus = false"
        @blur="userInputEvent('blur')"
        @mouseover="changeStatusTo('hover')"
        @mouseleave="changeStatusTo('blur')"
        @keypress="userInputEvent('keypress')" />
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'
import InputNumberStyle from '../../assets/style/components/InputNumber.module.scss'

const num = ref(0)
const ifFirstFocus = ref(true)
const checkInputStatus = ref('default')
const setInputValue = defineEmits(['setInputValue'])
const handleChange = (value) => {
    setInputValue('setInputValue', value)
}
const props = defineProps({
    disabled: Boolean,
    initValue: Number
})
// 控制輸入框狀態
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
            // showTips.value = true;
            changeStatusTo(inputStatus)
    },0)
}
// 父層傳入的初始值
num.value = props.initValue;

</script>
<style lang="scss">
@import '../../assets/style/variable.scss';
.InputNumber{
    border-radius: 5px;
    &.focus{
        @extend .default-input-outline--focus;
        // border:.1px $default-input-outline-color--hover solid;
        // box-shadow: 0px 0px 16px 0px rgba(0, 0, 0, 0.2);
    }
    &.hover{
        @extend .default-input-outline--hover;
        // box-shadow: 0 0 0 1px $default-input-outline-color--hover;
    }
    &.is-disabled {
        @extend .bg-disabled;
        // background: $default-input-background-color--disabled !important;
    }

}
</style>