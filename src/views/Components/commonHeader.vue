<template>
  <div class="bg-blue-300 rounded-md p-3 flex justify-between">
    <!-- 左侧 -->
    <div class="flex items-center">
      <div
        class="w-16 h-16 bg-yellow-300 rounded-full text-center leading-10 ml-6"
      >
        图片
      </div>
      <div class="flex flex-col ml-2 text-white text-sm">
        <span>系统管理员 admin</span>
        <span>系统管理员 集团总部·集团总部·前台管理员</span>
      </div>
    </div>
    <!-- 右侧 -->
    <div class="flex flex-col">
      <div class="text-white flex justify-between">
        <span> 早上好，系统管理员！今天是 2022年3月30日 星期三</span>
        <el-button color="#007bd8">
          <span class="text-white">设置座右铭</span>
        </el-button>
      </div>
      <div class="text-white mt-2">
        才华并不能使你坚韧不拔，宝剑锋从磨砺出，有辉煌成就的那些人，大抵都是用毅力获得成功的吧
      </div>
      <div class="flex mt-2">
        <div class="h-8 bg-yellow-200 rounded-2xl text-red-300 pt-1 pl-4 pr-4">
          今日工资 ：100元
        </div>
        <div
          class="h-8 bg-yellow-200 rounded-2xl text-red-300 ml-3 pt-1 pl-4 pr-4"
        >
          本月累计工资 ：2000元
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  name: '',
  setup() {
    return {}
  }
})
</script>
<style scoped></style>
