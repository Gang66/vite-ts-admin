<template>
  <div class="Nav-SecondNav-ThirdNav-index flex">
    <div class="mt-5 w-3/4">
      <common-header-vue />
      <div class="mt-4">
        <el-card>
          <div class="flex justify-between">
            <div>
              <span
                class="mr-2 cursor-pointer"
                :class="{ activeIndex: currentIndex === 1 }"
                @click="changeTitle(1)"
                >课件素材</span
              >
              <span
                class="mr-2 cursor-pointer"
                :class="{ activeIndex: currentIndex === 2 }"
                @click="changeTitle(2)"
                >成品课件</span
              >
              <span
                class="mr-2 cursor-pointer"
                :class="{ activeIndex: currentIndex === 3 }"
                @click="changeTitle(3)"
                >试题库</span
              >
              <span
                class="cursor-pointer"
                :class="{ activeIndex: currentIndex === 4 }"
                @click="changeTitle(4)"
                >试题纠错</span
              >
            </div>
            <div class="titleInput flex">
              <el-input class="mr-2" placeholder="课程名称"></el-input>
              <el-select class="mr-2"></el-select>
              <el-select class="mr-2" placeholder="搜索等级"></el-select>
              <el-button class="mr-2" type="primary">搜索</el-button>
              <el-button
                type="primary"
                @click="showmateria"
                v-if="showBtn === 1"
                >上传素材</el-button
              >
              <el-button
                type="danger"
                @click="showmateria"
                v-else-if="showBtn === 2"
                >下架课程</el-button
              >
            </div>
          </div>
          <!-- 表格内容 -->
          <div class="tableColor m-2">
            <el-table
              :data="tableData"
              style="width: 100%"
              :header-cell-style="{
                'font-size': '16px',
                padding: '0px',
                background: '#4372e3',
                color: '#fff',
                height: '44px',
                fontWeight: '500'
              }"
            >
              <el-table-column type="index" label="序号" width="100" />
              <el-table-column prop="date" label="上传日期" width="150" />
              <el-table-column prop="name" label="课程名称" width="180" />
              <el-table-column prop="type" label="课程类型" width="180" />
              <el-table-column prop="grade" label="课程等级" width="180" />
              <el-table-column prop="Developer" label="开发者" width="150" />
              <el-table-column prop="duration" label="学习时长" width="150" />
              <el-table-column prop="address" label="操作">
                <template #default="{ row }">
                  <el-button type="text">预览</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="flex justify-end mt-2">
              <el-pagination
                v-model:currentPage="query.currentPage"
                v-model:page-size="query.pageSize"
                :page-sizes="[10, 15, 20, 30]"
                layout="total, sizes, prev, pager, next, jumper"
                :total="tableData.length"
              />
            </div>
          </div>
          <materiaDialog :data="data" @closematerial="closematerial" />
        </el-card>
      </div>
    </div>
    <div class="mt-5 ml-3 w-1/5 rounded-md">
      <rightDialogVue />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import rightDialogVue from '/@/views/Components/rightDialog.vue'
import commonHeaderVue from '/@/views/Components/commonHeader.vue'
import materiaDialog from './components/materialDialog.vue'
const materiaData = () => {
  const data = reactive({
    dialogVisible: false
  })
  //   点击上传素材
  const showmateria = () => {
    data.dialogVisible = true
  }
  // 接受子组件传来取消时间
  const closematerial = () => {
    data.dialogVisible = false
  }
  return { data, showmateria, closematerial }
}
export default defineComponent({
  name: 'ThirdNav',
  components: {
    commonHeaderVue,
    rightDialogVue,
    materiaDialog
  },
  setup(prop, context) {
    //   控制高亮显示
    const currentIndex = ref(1)
    // 控制显示不同内容的字段
    const showBtn = ref(1)
    // 点击切换高亮并且显示相应内容
    const changeTitle = (val: any) => {
      showBtn.value = val
      if (val === 1) {
        tableData.value = tableData1
      } else if (val === 2) {
        tableData.value = tableData2
      } else if (val === 3) {
        tableData.value = tableData3
      } else if (val === 4) {
        tableData.value = tableData4
      }
      currentIndex.value = val
    }
    // 表格数据
    const tableData1 = [
      {
        date: '2016-05-03',
        name: '11阀门故事会1',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-02',
        name: '阀门故事会2',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-04',
        name: '阀门故事会3',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-01',
        name: '阀门故事会4',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      }
    ]
    const tableData2 = [
      {
        date: '2016-05-03',
        name: '22阀门故事会1',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-02',
        name: '阀门故事会2',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-04',
        name: '阀门故事会3',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-01',
        name: '阀门故事会4',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      }
    ]
    const tableData3 = [
      {
        date: '2016-05-03',
        name: '33阀门故事会1',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-02',
        name: '阀门故事会2',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-04',
        name: '阀门故事会3',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-01',
        name: '阀门故事会4',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      }
    ]
    const tableData4 = [
      {
        date: '2016-05-03',
        name: '44阀门故事会1',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-02',
        name: '阀门故事会2',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-04',
        name: '阀门故事会3',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-01',
        name: '阀门故事会4',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      }
    ]
    const tableData = ref([
      {
        date: '2016-05-03',
        name: '11阀门故事会1',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-02',
        name: '阀门故事会2',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-04',
        name: '阀门故事会3',
        type: '技术类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      },
      {
        date: '2016-05-01',
        name: '阀门故事会4',
        type: '通用类',
        grade: '初级',
        Developer: '管理员',
        duration: '1分钟'
      }
    ])
    // 分页
    const query = reactive({
      currentPage: 1,
      pageSize: 10
    })
    return {
      ...materiaData(),
      currentIndex,
      changeTitle,
      tableData,
      query,
      showBtn
    }
  }
})
</script>
<style lang="postcss" scoped>
.Nav-SecondNav-ThirdNav-index {
  .tableColor {
    :deep(.el-table__header) {
      background-color: red;
    }
  }
  .activeIndex {
    color: #409eff;
    font-size: 18px;
  }
  .titleInput {
    :deep(.el-input__inner) {
      width: 120px;
    }
  }
}
</style>
