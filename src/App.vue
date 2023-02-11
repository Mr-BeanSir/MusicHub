<script setup>
import { RouterView } from "vue-router";
import "reset-css/reset.css";
import HeaderComponents from "@/components/HeaderComponents.vue";
</script>

<template>
  <el-container class="container">
    <el-header class="app-header"><HeaderComponents /></el-header>
    <el-main class="app-main"><RouterView /></el-main>
    <el-footer class="app-footer">Footer</el-footer>
  </el-container>
</template>

<style scoped>
.container {
  display: flex;
  align-items: center;
}
.app-header,
.app-main,
.app-footer {
  width: 1024px;
}
</style>
