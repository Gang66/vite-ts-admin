<template>
  <div>
    <el-dialog
      v-model="data.dialogVisible"
      width="800px"
      custom-class="dialogClass"
      @closed="closedOne"
    >
      <div
        class="w-full bg-blue-400 text-white pl-6"
        style="height: 40px; line-height: 40px"
      >
        工作总结
      </div>
      <!-- 今日数据内容 -->
      <div>
        <!-- 今日数据表头 -->
        <div class="flex justify-between">
          <div class="flex mt-4">
            <div class="w-6 h-6 mt-2">
              <img src="../../../assets/img/circle.png" alt="" />
            </div>
            <div class="ml-2">
              <span class="text-lg font-black">今日数据 </span>
              <span> 数据说话，言之凿凿</span>
            </div>
          </div>
          <div class="mt-4">
            <a href="javascript:;" class="text-red-400" @click="putAway"
              >收起</a
            >
          </div>
        </div>
        <!-- 每个时间内容 -->
        <div class="flex mt-1" v-if="showNowdata">
          <!-- 左侧时间 -->
          <div class="flex-1">
            <div class="flex">
              <div>上午时间</div>
              <div class="ml-16">工作记录及事项</div>
            </div>
            <div
              class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
            >
              <div class="w-1/4 bg-gray-100 flex items-center p-1">
                <span> 08:00~09:00</span>
              </div>
              <div class="w-3/4 flex justify-between items-center">
                <span></span>
                <span class="mr-1" @click="openchildDialog">
                  <img src="../../../assets/img/add.png" alt="" class="w-4"
                /></span>
              </div>
            </div>
            <div
              class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
            >
              <div class="w-1/4 bg-gray-100 flex items-center p-1">
                <span> 09:00~10:00</span>
              </div>
              <div class="w-3/4 flex justify-between items-center">
                <span></span>
                <span class="mr-1" @click="openchildDialog">
                  <img src="../../../assets/img/add.png" alt="" class="w-4"
                /></span>
              </div>
            </div>
            <div
              class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
            >
              <div class="w-1/4 bg-gray-100 flex items-center p-1">
                <span> 10:00~11:00</span>
              </div>
              <div class="w-3/4 flex justify-between items-center">
                <span></span>
                <span class="mr-1" @click="openchildDialog">
                  <img src="../../../assets/img/add.png" alt="" class="w-4"
                /></span>
              </div>
            </div>
            <div
              class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
            >
              <div class="w-1/4 bg-gray-100 flex items-center p-1">
                <span> 11:00~12:00</span>
              </div>
              <div class="w-3/4 flex justify-between items-center">
                <span></span>
                <span class="mr-1" @click="openchildDialog">
                  <img src="../../../assets/img/add.png" alt="" class="w-4"
                /></span>
              </div>
            </div>
          </div>
          <!-- 右侧时间 -->
          <div class="flex-1 ml-2">
            <div class="flex">
              <div>上午时间</div>
              <div class="ml-16">工作记录及事项</div>
            </div>
            <div
              class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
            >
              <div class="w-1/4 bg-gray-100 flex items-center p-1">
                <span> 13:00~14:00</span>
              </div>
              <div class="w-3/4 flex justify-between items-center">
                <span></span>
                <span class="mr-1" @click="openchildDialog">
                  <img src="../../../assets/img/add.png" alt="" class="w-4"
                /></span>
              </div>
            </div>
            <div
              class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
            >
              <div class="w-1/4 bg-gray-100 flex items-center p-1">
                <span> 14:00~15:00</span>
              </div>
              <div class="w-3/4 flex justify-between items-center">
                <span></span>
                <span class="mr-1" @click="openchildDialog">
                  <img src="../../../assets/img/add.png" alt="" class="w-4"
                /></span>
              </div>
            </div>
            <div
              class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
            >
              <div class="w-1/4 bg-gray-100 flex items-center p-1">
                <span> 15:00~16:00</span>
              </div>
              <div class="w-3/4 flex justify-between items-center">
                <span></span>
                <span class="mr-1" @click="openchildDialog">
                  <img src="../../../assets/img/add.png" alt="" class="w-4"
                /></span>
              </div>
            </div>
            <div
              class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
            >
              <div class="w-1/4 bg-gray-100 flex items-center p-1">
                <span> 16:00~17:00</span>
              </div>
              <div class="w-3/4 flex justify-between items-center">
                <span></span>
                <span class="mr-1" @click="openchildDialog">
                  <img src="../../../assets/img/add.png" alt="" class="w-4"
                /></span>
              </div>
            </div>
          </div>
        </div>
        <!-- 子组件Dialog -->
        <childrenDialogVue :childata="showChilDialog" @closed="closed" />
      </div>
      <template #footer>
        <span class="dialog-footer">
          <el-button @click="closes">关闭</el-button>
          <el-button type="primary" @click="dialogVisible = false"
            >提交</el-button
          >
        </span>
      </template>
    </el-dialog>
  </div>
</template>
<script lang="ts">
import { defineComponent, SetupContext, ref, reactive } from 'vue'
import childrenDialogVue from './childrenDialog.vue'
export default defineComponent({
  name: '',
  components: {
    childrenDialogVue
  },
  props: {
    data: {
      type: Object
    }
  },
  emits: ['close'],
  setup(prop, SetupContext) {
    //   点击收起今日数据
    const showNowdata = ref(false)
    const putAway = () => {
      showNowdata.value = !showNowdata.value
    }
    // 发送关闭事件给父组件
    const closes = () => {
      SetupContext.emit('close')
    }
    // 打开子组件的dialog
    const openchildDialog = () => {
      showChilDialog.isOpen = true
    }
    // 子组件是否打开,子组件传值
    const showChilDialog = reactive({
      isOpen: false
    })
    // 接受子组件发送的事件
    const closed = () => {
      showChilDialog.isOpen = false
    }
    // 关闭dialog
    const closedOne = () => {
      showNowdata.value = false
    }
    return {
      closedOne,
      closes,
      putAway,
      showNowdata,
      showChilDialog,
      openchildDialog,
      closed
    }
  }
})
</script>
<style lang="postcss" scoped>
.dialogClass {
  :deep(.el-dialog__body) {
    padding: 0;
  }
}
</style>
