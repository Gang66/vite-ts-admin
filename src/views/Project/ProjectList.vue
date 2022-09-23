<template>
  <div class="flex">
    <div class="mt-10 w-3/4">
      <el-card class="box-card">
        <div class="flex justify-between">
          <span class="text-blue-400">创新举措</span>
          <span>
            <el-select placeholder="创建时间" style="width: 150px"></el-select>
            <el-select placeholder="字典状态" style="width: 150px"></el-select>
            <el-button type="primary" style="margin-left: 20px">搜索</el-button>
            <el-button type="primary" @click="openHrDialog">新增</el-button>
          </span>
        </div>
        <div class="mt-3">
          <el-table
            :header-cell-style="{ background: '#4372e3', color: '#fff' }"
            :data="tableData"
            style="width: 100%"
          >
            <el-table-column type="index" label="序号" width="100" />
            <el-table-column prop="date" label="创建时间" width="130" />
            <el-table-column prop="type" label="建议类型" width="130" />
            <el-table-column prop="name" label="建议人" width="130" />
            <el-table-column
              :show-overflow-tooltip="true"
              prop="form.needs"
              label="建议内容"
              width="130"
            />
            <el-table-column label="处理状态" width="130" />
            <el-table-column prop="name" label="处理人" width="130" />
            <el-table-column prop="content" label="处理内容">
              <template #default="{ row }">
                <el-button type="text" @click="hasDialog(row)">
                  <!-- {{ row.form }} -->
                  {{ row.form.needs }}
                </el-button>
              </template>
            </el-table-column>
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
            :total="tableData.length"
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
          />
        </div>
      </el-card>
      <innovationDialog
        :data="innovationData"
        @closed="closed"
        v-if="innovationData.isShow"
      />
    </div>
    <!-- =右侧所有内容 -->
    <div class="mt-10 ml-3 w-1/5 rounded-md"><rightDialog /></div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, watch } from 'vue'
import innovationDialog from './components/innovationDialog.vue'
import rightDialog from '/@/views/Components/rightDialog.vue'
// 创新举措
const innTable = () => {
  // 右侧点击打开dialog
  const rightbtn = (val: any) => {
    innovationData.userInfo.number = val
    innovationData.dialogVisible = true
  }
  // 点击打开dialog
  const openHrDialog = () => {
    innovationData.userInfo.number = '1'
    innovationData.isShow = true
    innovationData.dialogVisible = true
  }
  // 监听关闭按钮
  const closed = () => {
    innovationData.isShow = false
    innovationData.dialogVisible = false
  }
  // 分页器
  const currentPage4 = ref(1)
  const pageSize4 = ref(5)
  const handleSizeChange = (val: number) => {
    console.log(`${val} items per page`)
  }
  const handleCurrentChange = (val: number) => {
    console.log(`current page: ${val}`)
  }

  const innovationData = reactive({
    dialogVisible: false,
    isShow: false,
    userInfo: {
      number: '1',
      date: '',
      type: '',
      name: '',
      form: {
        // 需要什么样培训的内容
        needs: '',
        // 需要什么样的培训方式
        trainingMethod: '',
        // 对培训时间等的建议
        trainingSuggest: '',
        // 意见培训
        opinionTraining: '',
        // 创新举措
        innovativeInitiatives: '',
        // 其他建议
        otherSuggestion: '',
        checked: false
      }
    }
  })
  const tableData = [
    {
      date: '2016-05-03',
      type: '其他建议',
      name: '冯佳丽',
      form: {
        // 需要什么样培训的内容
        needs: '123',
        // 需要什么样的培训方式
        trainingMethod: '',
        // 对培训时间等的建议
        trainingSuggest: '',
        // 意见培训
        opinionTraining: '',
        // 创新举措
        innovativeInitiatives: '',
        // 其他建议
        otherSuggestion: '1113',
        checked: false
      },

      number: '4'
    },
    {
      date: '2016-05-02',
      type: '培训调研',
      name: '冯佳丽',
      form: {
        // 需要什么样培训的内容
        needs:
          '222某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某',
        // 需要什么样的培训方式
        trainingMethod: '222',
        // 对培训时间等的建议
        trainingSuggest: '222',
        // 意见培训
        opinionTraining: '222',
        // 创新举措
        innovativeInitiatives: '2223',
        // 其他建议
        otherSuggestion: '2224',
        checked: true
      },

      number: '1'
    },
    {
      date: '2016-05-04',
      type: '意见建议',
      name: '匿名',
      form: {
        // 需要什么样培训的内容
        needs:
          '333某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某',
        // 需要什么样的培训方式
        trainingMethod: '333某某某某某某',
        // 对培训时间等的建议
        trainingSuggest: '333某某某某某某1',
        // 意见培训
        opinionTraining: '333123',
        // 创新举措
        innovativeInitiatives: '3331231',
        // 其他建议
        otherSuggestion: '3331212232',
        checked: true
      },

      number: '2'
    },
    {
      date: '2016-05-01',
      type: '创新举措',
      name: '匿名',
      form: {
        // 需要什么样培训的内容
        needs:
          '444某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某某',
        // 需要什么样的培训方式
        trainingMethod: '444某某某某某某',
        // 对培训时间等的建议
        trainingSuggest: '444某某某某某某1',
        // 意见培训
        opinionTraining: '444123',
        // 创新举措
        innovativeInitiatives: '4441231',
        // 其他建议
        otherSuggestion: '4441212232',
        // 是否是匿名
        checked: false
      },

      number: '3'
    }
  ]
  const hasDialog = (row: any) => {
    innovationData.userInfo = row
    innovationData.isShow = true
    innovationData.dialogVisible = true
  }
  return {
    rightbtn,
    tableData,
    hasDialog,
    innovationData,
    closed,
    openHrDialog,
    currentPage4,
    pageSize4,
    handleSizeChange,
    handleCurrentChange
  }
}
export default defineComponent({
  name: 'ProjectList',
  components: {
    innovationDialog,
    rightDialog
  },
  setup() {
    // 排行榜

    return {
      ...innTable()
    }
  }
})
</script>
<style>
.rightbut .el-button {
  color: white;
}
</style>
