<template>
    <el-button
        class="defaultButton"
        :class="[defaultButtonStyle.defaultButtonStyle, buttonSize]"
        type="primary"
        @click="submitData"
        :disabled="disabled">
        <div v-if="slots.left" class="icon-left">
            <slot name="left"></slot>
        </div>
        {{ title }}
        <div v-if="slots.right" class="icon-right">
            <slot name="right"></slot>
        </div>
        </el-button>
</template>
<script setup>
import defaultButtonStyle from '../../assets/style/components/defaultButton.module.scss'
import { defineEmits, defineProps, useSlots } from 'vue';
const props = defineProps({
    buttonSize: String,
    disabled: Boolean,
    title: String
})
const slots = useSlots();

const submit = defineEmits(['submit'])
function submitData(){
    submit('submit')
}


</script>
<style lang="scss">
@import '../../assets/style/variable.scss';
.defaultButton {
    .icon{
        &-left,
        &-right {
            width: 20px;
            height: 20px;
        }
        &-left {
            margin-right: 16px;
        }
        &-right {
            margin-left: 16px;
        }
    }
    &.large {
        font-size: 16px;
        // width: 87px;
        height: 48px;
        .icon{
            &-left,
            &-right {
                width: 24px;
                height: 24px;
            }
            &-left {
                margin-right: 12px;
            }
            &-right {
                margin-left: 12px;
            }
        }
    }
    &.small {
        // width: 73px;
        height: 32px;
        font-size: 12px;
        .icon{
            &-left,
            &-right {
                width: 14px;
                height: 17px;
            }
            &-left {
                margin-right: 12px;
            }
            &-right {
                margin-left: 12px;
            }
        }
    }
    &.is-disabled,
    &.is-disabled:hover{
        background-color: $default-button-background-color--disabled;
        color: $default-button-color--disabled;
        border-color: $default-button-background-color--disabled;
    }
}

</style>