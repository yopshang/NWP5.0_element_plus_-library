<template>
    <el-button
        class="defaultButton"
        :class="[defaultButtonStyle.defaultButtonStyle, buttonSize]"
        type="primary"
        @click="submitData">Button</el-button>
</template>
<script setup>
import defaultButtonStyle from '../../assets/style/components/defaultButton.module.scss'
import { defineEmits, defineProps } from 'vue';
const props = defineProps({
    buttonSize: String
})
const submit = defineEmits(['submit'])
function submitData(){
    submit('submit')
}


</script>
<style lang="scss">
@import '../../assets/style/variable.scss';
.defaultButton {
    &.large {
        width: 87px;
        height: 48px;
    }
    &.small {
        width: 73px;
        height: 32px;
    }
}

</style>