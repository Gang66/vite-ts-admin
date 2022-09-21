<template>
  <div class="chilDialog">
    <el-dialog v-model="childata.isOpen" width="30%">
      <!-- 头部 -->
      <div
        class="bg-blue-600 w-full h-10 flex justify-between items-center pl-2"
      >
        <h2 class="text-white">添加工作内容</h2>
        <div class="mr-1 flex items-center">
          <div>
            <el-button size="mini" type="primary">提交</el-button>
          </div>
          <div
            class="h-5 w-5 bg-slate-300 ml-2 rounded-full flex items-center justify-center"
            @click="close"
          >
            <span class="text-lg text-white">×</span>
          </div>
        </div>
      </div>
      <!-- 内容 -->
      <div class="p-4">
        <div class="flex">
          <span>工作日期</span>
          <span class="ml-2 font-extrabold">2022-09-21</span>
        </div>
        <div>
          <div><span>工作时间</span></div>
          <div class="unline">
            <span>08时</span>
            <el-input></el-input>
          </div>
        </div>
      </div>
    </el-dialog>
  </div>
</template>
<script lang="ts">
import { defineComponent, SetupContext } from 'vue'
export default defineComponent({
  name: '',
  props: {
    childata: {
      type: Object
    }
  },
  emits: ['closed'],
  setup(prop, SetupContext) {
    const close = () => {
      SetupContext.emit('closed')
    }
    return { close }
  }
})
</script>
<style lang="postcss" scoped>
.chilDialog {
  :deep(.el-input__inner) {
    width: 60px;
    border-top-width: 0px;
    border-left-width: 0px;
    border-right-width: 0px;
    border-bottom-width: 1px;
  }
  :deep(.el-dialog__body) {
    padding: 0;
  }
}
</style>
