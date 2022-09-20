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
                  {{ row.form.needs }}</el-button
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
      <innovationDialog :data="innovationData" @closed="closed" />
    </div>
    <!-- =右侧所有内容 -->
    <div class="mt-10 ml-3 w-1/5 rounded-md">
      <!-- 创新直通车 -->
      <div class="rounded-md bg-white h-40">
        <div class="w-full h-10 bg-blue-400 rounded-md leading-10 pl-3">
          <span class="text-white">创新直通车</span>
        </div>
        <div class="rightbut flex flex-col mt-3">
          <div class="w-full ml-6">
            <el-button
              @click="rightbtn('1')"
              style="width: 40%; height: 40px"
              round
              color="#00abff"
              >培训调研</el-button
            >
            <el-button
              @click="rightbtn('2')"
              style="width: 40%; height: 40px"
              round
              color="#f6bc00"
              >意见建议</el-button
            >
          </div>
          <div class="mt-3 w-full ml-6">
            <el-button
              @click="rightbtn('3')"
              style="width: 40%; height: 40px"
              round
              color="#57d7fd"
              >创新举措</el-button
            >
            <el-button
              @click="rightbtn('4')"
              style="width: 40%; height: 40px"
              round
              color="#1fedcb"
              >其他建议</el-button
            >
          </div>
        </div>
      </div>
      <!-- 常用工具 -->
      <div class="rounded-md bg-white mt-3">
        <div class="w-full h-10 bg-blue-400 rounded-md leading-10 pl-3">
          <span class="text-white">常用工具</span>
        </div>
        <div class="flex flex-wrap p-2">
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
        </div>
      </div>
      <!-- 排行榜 -->
      <div class="rounded-md bg-white mt-3">
        <div class="w-full h-10 bg-blue-400 rounded-md leading-10 pl-3">
          <span class="text-white">排行榜</span>
        </div>
        <div class="pl-4 pb-3">
          <el-tabs
            v-model="activeName"
            class="demo-tabs"
            @tab-click="handleClick"
          >
            <el-row class="text-center mb-2">
              <el-col :span="5"><span class="font-black">排名</span></el-col>
              <el-col :span="8"><span class="font-black">事业部</span></el-col>
              <el-col :span="8"
                ><span class="font-black">培训专员</span></el-col
              >
            </el-row>
            <el-tab-pane label="邀约排行" name="first">
              <div>
                <el-row class="text-center">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      1
                    </div></el-col
                  >
                  <el-col :span="8"><span>集团总部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      2
                    </div></el-col
                  >
                  <el-col :span="8"><span>潍坊事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      3
                    </div></el-col
                  >
                  <el-col :span="8"><span>济南事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      4
                    </div></el-col
                  >
                  <el-col :span="8"><span>润扬事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      5
                    </div></el-col
                  >
                  <el-col :span="8"><span>南京事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      6
                    </div></el-col
                  >
                  <el-col :span="8"><span>银川事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      7
                    </div></el-col
                  >
                  <el-col :span="8"><span>邯郸事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      8
                    </div></el-col
                  >
                  <el-col :span="8"><span>湖高事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      9
                    </div></el-col
                  >
                  <el-col :span="8"><span>北京事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      10
                    </div></el-col
                  >
                  <el-col :span="8"><span>寒亭事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
              </div>
            </el-tab-pane>
            <el-tab-pane label="面试排行" name="second">
              <div>
                <el-row class="text-center">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      1
                    </div></el-col
                  >
                  <el-col :span="8"><span>寒亭总部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      2
                    </div></el-col
                  >
                  <el-col :span="8"><span>潍坊事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      3
                    </div></el-col
                  >
                  <el-col :span="8"><span>济南事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      4
                    </div></el-col
                  >
                  <el-col :span="8"><span>润扬事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      5
                    </div></el-col
                  >
                  <el-col :span="8"><span>南京事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      6
                    </div></el-col
                  >
                  <el-col :span="8"><span>银川事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      7
                    </div></el-col
                  >
                  <el-col :span="8"><span>邯郸事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      8
                    </div></el-col
                  >
                  <el-col :span="8"><span>湖高事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      9
                    </div></el-col
                  >
                  <el-col :span="8"><span>北京事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      10
                    </div></el-col
                  >
                  <el-col :span="8"><span>集团事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
              </div>
            </el-tab-pane>
          </el-tabs>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, watch } from 'vue'
import innovationDialog from './components/innovationDialog.vue'
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
    innovationData.dialogVisible = true
  }
  // 监听关闭按钮
  const closed = () => {
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
    userInfo: {
      number: '1'
    }
  })
  const tableData = [
    {
      date: '2016-05-03',
      type: '其他建议',
      name: '冯佳丽',
      form: {
        // 需要什么样培训的内容
        needs: '111某某某123',
        // 需要什么样的培训方式
        trainingMethod: '111某某某某某某',
        // 对培训时间等的建议
        trainingSuggest: '111某某某某某某1',
        // 意见培训
        opinionTraining: '111',
        // 创新举措
        innovativeInitiatives: '112',
        // 其他建议
        otherSuggestion: '1113',
        checked: true
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
    innovationData.dialogVisible = true
    // console.log(row)
    innovationData.userInfo = row
    // console.log(innovationData.userInfo)
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
    innovationDialog
  },
  setup() {
    // 排行榜
    const activeName = ref('first')
    return {
      activeName,
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
