<template>
    <el-col :span="8" :class="LayoutStyle['layout-bottom-gutter']">
        <slot>
        </slot>
    </el-col>
</template>
<script setup>
import LayoutStyle from '../assets/style/Layout.module.scss'
</script>