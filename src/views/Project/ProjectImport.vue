<template>
  <div class="project-project-import flex">
    <div class="mt-5 w-3/4">
      <!-- 头部 -->
      <commonHeaderVue />
      <!-- tab栏切换 -->
      <el-card class="mt-3">
        <div class="flex justify-between">
          <div class="flex">
            <a
              href="javascript:;"
              @click="untrial"
              :class="{ 'text-red-300': currentIndex === '1' }"
              >未审</a
            >
            <a
              href="javascript:;"
              class="ml-2"
              @click="Tried"
              :class="{ 'text-red-300': currentIndex === '2' }"
              >已审</a
            >
            <a
              href="javascript:;"
              class="ml-2"
              @click="notWritten"
              :class="{ 'text-red-300': currentIndex === '3' }"
              >未写</a
            >
          </div>
          <div class="flex">
            <el-input
              placeholder="姓名"
              style="width: 100px; margin-right: 10px"
            />
            <el-button type="primary">搜索</el-button>
            <el-button type="primary" @click="SummarizeDialog"
              >写总结</el-button
            >
          </div>
        </div>
        <!-- tab列表 -->
        <div class="mt-3">
          <el-table
            :data="tableData1"
            style="width: 100%"
            :header-cell-style="{ background: '#4372e3', color: '#fff' }"
          >
            <el-table-column type="index" label="序号" width="100" />
            <el-table-column prop="date" label="日期" width="110" />
            <el-table-column prop="department" label="部门" width="170" />
            <el-table-column prop="name" label="姓名" width="100" />
            <el-table-column prop="type" label="总结类型" width="100" />
            <el-table-column prop="state" label="总结状态" width="100" />
            <el-table-column prop="saturation" label="饱和度" width="100" />
            <el-table-column
              prop="efficiency"
              label="工作自评效率"
              width="100"
            />
            <el-table-column prop="quality" label="质量" width="100" />
            <el-table-column
              prop="ApprovalStatus"
              label="审批状态"
              width="100"
            />
            <el-table-column label="操作" width="100">
              <template #default="{ row }">
                <el-button type="text" @click="SummarizeDialog(row)"
                  >审阅</el-button
                >
              </template>
            </el-table-column>
          </el-table>
        </div>
        <div class="flex justify-end">
          <el-pagination
            v-model:currentPage="currentPage4"
            v-model:page-size="pageSize4"
            :page-sizes="[5, 10, 20, 30]"
            layout="total, sizes, prev, pager, next, jumper"
            :total="tableData1.length"
          />
        </div>
        <SummarizeDialogVue :data="SummarizeData" @close="close" />
      </el-card>
    </div>
    <div class="mt-5 ml-3 w-1/5 rounded-md">
      <rightDialog />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import rightDialog from '/@/views/Components/rightDialog.vue'
import SummarizeDialogVue from './components/SummarizeDialog.vue'
import commonHeaderVue from '../Components/commonHeader.vue'
export default defineComponent({
  name: 'ProjectImport',
  components: {
    rightDialog,
    SummarizeDialogVue,
    commonHeaderVue
  },

  setup() {
    //   监听关系按钮
    const close = () => {
      SummarizeData.dialogVisible = false
    }
    //   打开写总结dialog
    const SummarizeDialog = () => {
      SummarizeData.dialogVisible = true
    }
    const SummarizeData = reactive({
      dialogVisible: false
    })

    const fromInfro = reactive({
      list: [],
      q: {
        currentIndex: 100,
        currentPage4: 1,
        pageSize4: 10
      }
    })
    // table表单的数据
    const tableData1 = [
      {
        date: '2022-09-24',
        name: '系统管理员',
        department: '集团总部',
        type: '日总结',
        state: '正式期',
        saturation: '好',
        efficiency: '好',
        quality: '好',
        ApprovalStatus: '未审阅'
      },
      {
        date: '2022-09-24',
        name: '系统管理员',
        department: '集团总部',
        type: '日总结',
        state: '正式期',
        saturation: '好',
        efficiency: '好',
        quality: '好',
        ApprovalStatus: '未审阅'
      },
      {
        date: '2022-09-24',
        name: '系统管理员',
        type: '日总结',
        department: '集团总部',
        state: '正式期',
        saturation: '好',
        efficiency: '好',
        quality: '好',
        ApprovalStatus: '未审阅'
      },
      {
        date: '2022-09-24',
        name: '系统管理员',
        type: '日总结',
        department: '集团总部',
        state: '正式期',
        saturation: '好',
        efficiency: '好',
        quality: '好',
        ApprovalStatus: '未审阅'
      }
    ]
    // 分页
    const currentIndex = ref('1')
    const currentPage4 = ref(1)
    const pageSize4 = ref(5)

    const untrial = () => {
      currentIndex.value = '1'
    }
    const Tried = () => {
      currentIndex.value = '2'
    }
    const notWritten = () => {
      currentIndex.value = '3'
    }
    return {
      close,
      SummarizeDialog,
      SummarizeData,
      pageSize4,
      tableData1,
      currentIndex,
      untrial,
      Tried,
      notWritten,
      currentPage4
    }
  }
})
</script>
<style lang="postcss" scoped>
.project-project-import {
}
</style>
