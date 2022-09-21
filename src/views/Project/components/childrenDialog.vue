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
      <div class="p-4 w-full">
        <!-- 日期 -->
        <div class="flex">
          <span>工作日期</span>
          <span class="ml-2 font-extrabold">2022-09-21</span>
        </div>
        <!-- 时间 -->
        <div class="flex items-center mt-6">
          <div>
            <span>工作时间</span>
          </div>
          <div class="unline w-200 flex items-center ml-2">
            <span>08时</span>
            <span class="ml-1"
              ><el-input type="number" v-model="data.start"></el-input
            ></span>
            <span>分至</span>
            <span class="ml-1"
              ><el-input type="number" v-model="data.end"></el-input
            ></span>
            <span>分</span>
          </div>
        </div>
        <!-- 内容 -->
        <div class="w-200 flex items-center mt-6">
          <span>工作内容</span>
          <span class="ml-1 contants"
            ><el-input
              v-model="data.contant"
              placeholder="请输入工作内容"
            ></el-input
          ></span>
        </div>
      </div>
    </el-dialog>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, SetupContext } from 'vue'
export default defineComponent({
  name: '',
  props: {
    childata: {
      type: Object
    }
  },
  emits: ['closed'],
  setup(prop, SetupContext) {
    const data = reactive({
      start: '',
      end: '',
      contant: ''
    })
    const close = () => {
      SetupContext.emit('closed')
    }
    return { close, data }
  }
})
</script>
<style lang="postcss" scoped>
.chilDialog {
  .contants {
    :deep(.el-input__inner) {
      width: 200px;
    }
  }
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
