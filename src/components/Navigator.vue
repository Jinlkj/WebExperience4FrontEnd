<template>
  <div aria-label="A complete example of page header">
    <el-page-header @back="onBack">
      <template #breadcrumb>
        <el-breadcrumb separator="/">
          <el-breadcrumb-item :to="{ path: './page-header.html' }">
            第四次web实验
          </el-breadcrumb-item>
        </el-breadcrumb>
      </template>
      <template #content>
        <div class="flex items-center">
          <el-avatar
              class="mr-3"
              :size="32"
              src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png"
          />
          <span class="text-large font-600 mr-3"> 夏劲 </span>
          <span
              class="text-sm mr-2"
              style="color: var(--el-text-color-regular)"
          >
            软工3班
          </span>
          <el-tag>大数据与软件学院</el-tag>
        </div>
      </template>
      <template #extra>
      </template>
      <el-descriptions :column="3" size="small" class="mt-4">
        <el-descriptions-item label="用户名"
        >夏劲</el-descriptions-item
        >
        <el-descriptions-item label="电话"
        >13364030920</el-descriptions-item
        >
        <el-descriptions-item label="城市">重庆</el-descriptions-item>
        <el-descriptions-item label="标签">
          <el-tag size="small">学生</el-tag>
        </el-descriptions-item>
        <el-descriptions-item label="地址"
        >重庆大学（虎溪校区），重庆
        </el-descriptions-item>
      </el-descriptions>
    </el-page-header>
  </div>
</template>

<script setup lang="ts">
import { ElNotification as notify } from 'element-plus'

const onBack = () => {
  notify('Back')
}
</script>
