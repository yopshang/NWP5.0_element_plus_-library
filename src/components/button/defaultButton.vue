<template>
    <el-button
        class="customButton"
        :class="[buttonStyle.button, buttonSize]"
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
import primaryButtonStyle from '../../assets/style/components/primaryButton.module.scss';
import secondaryButtonStyle from '../../assets/style/components/secondaryButton.module.scss';
import { defineEmits, defineProps, useSlots, reactive, computed } from 'vue';
const props = defineProps({
    buttonSize: String,
    disabled: Boolean,
    title: String,
    buttonType: String,
})
const slots = useSlots();
const buttonStyle = reactive(
    computed(() => {
        switch(props.buttonType){
            case 'primaryButtonStyle':
                return primaryButtonStyle;
            case 'secondaryButtonStyle':
                return secondaryButtonStyle
            default:
                return primaryButtonStyle;
        }
    })
)
console.log('primaryButtonStyle:', primaryButtonStyle);
console.log('secondaryButtonStyle:', secondaryButtonStyle);


const submit = defineEmits(['submit'])
function submitData(){
    submit('submit')
}



</script>
<style lang="scss">
@import '../../assets/style/variable.scss';
.customButton {
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
        @extend .bg-disabled, .border-disabled, .text-disabled;
        svg {
            // fill: red;
        }
    }
}

</style>