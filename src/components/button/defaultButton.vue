<template>
    <el-button
        :class="defaultButtonStyle.defaultButtonStyle"
        type="primary"
        @click="submitData">Button</el-button>
</template>
<script setup>
import defaultButtonStyle from '../../assets/style/components/defaultButton.module.scss'
import { defineEmits } from 'vue';

const submit = defineEmits(['submit'])
function submitData(){
    submit('submit')
}


</script>
<style lang="scss">
@import '../../assets/style/variable.scss';

</style>