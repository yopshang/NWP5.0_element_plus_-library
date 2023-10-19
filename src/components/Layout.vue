<template>
    <el-col :span="8" :class="LayoutStyle['mb-4']">
        <slot>
        </slot>
    </el-col>
</template>
<script setup>
import LayoutStyle from '../assets/style/Layout.module.scss'
</script>