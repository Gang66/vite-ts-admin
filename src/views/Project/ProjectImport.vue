<template>
  <div class="project-project-import flex">
    <div class="mt-10 w-3/4">
      <!-- 头部 -->
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
            <div
              class="h-8 bg-yellow-200 rounded-2xl text-red-300 pt-1 pl-4 pr-4"
            >
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
            <el-table-column prop="date" label="序号" width="100" />
            <el-table-column prop="name" label="日期" width="100" />
            <el-table-column prop="address" label="部门" width="180" />
            <el-table-column prop="address" label="姓名" width="100" />
            <el-table-column prop="address" label="总结类型" width="100" />
            <el-table-column prop="address" label="总结状态" width="100" />
            <el-table-column prop="address" label="饱和度" width="100" />
            <el-table-column prop="address" label="工作自评效率" width="100" />
            <el-table-column prop="address" label="质量" width="100" />
            <el-table-column prop="address" label="审批状态" width="100" />
            <el-table-column prop="address" label="操作" width="100" />
          </el-table>
        </div>
        <div class="flex justify-end">
          <el-pagination
            v-model:currentPage="currentPage4"
            v-model:page-size="pageSize4"
            :page-sizes="[5, 10, 20, 30]"
            :small="small"
            :disabled="disabled"
            :background="background"
            layout="total, sizes, prev, pager, next, jumper"
            :total="tableData1.length"
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
          />
        </div>
        <SummarizeDialogVue :data="SummarizeData" @close="close" />
      </el-card>
    </div>
    <div class="mt-10 ml-3 w-1/5 rounded-md"><rightDialog /></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import rightDialog from '/@/views/Components/rightDialog.vue'
import SummarizeDialogVue from './components/SummarizeDialog.vue'

export default defineComponent({
  name: 'ProjectImport',
  components: {
    rightDialog,
    SummarizeDialogVue
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
      currentIndex: 100,
      currentPage4: 1,
      pageSize4: 10
    })
    const tableData1 = [
      {
        date: '2016-05-03',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles'
      },
      {
        date: '2016-05-02',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles'
      },
      {
        date: '2016-05-04',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles'
      },
      {
        date: '2016-05-01',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles'
      }
    ]
    const currentIndex = ref('1')
    // 分页
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
