<template>
  <div class="assetsa-assetProcurement-components-purchaseTable">
    <div class="flex justify-between">
      <h2>资产采购</h2>
      <div class="flex changeType">
        <el-select v-model="formdata.head" class="firstSelect">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          />
        </el-select>
        <el-input
          v-if="formdata.head === 'name'"
          placeholder="请输入搜索内容"
          v-model="formdata.contant"
        ></el-input>
        <el-date-picker
          v-else-if="formdata.head === 'times'"
          v-model="formdata.dates"
          type="daterange"
          range-separator="-"
          start-placeholder="开始时间"
          end-placeholder="结束时间"
        />
        <el-select
          v-else-if="formdata.head === 'channel'"
          v-model="formdata.channel"
          ><el-option
            v-for="item in options1"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          />
        </el-select>
        <el-button
          style="margin-left: 20px; color: #468bfd; border: 1px solid #468bfd"
          >查询</el-button
        >
        <el-button type="primary" @click="addAssets">资产申请</el-button>
      </div>
    </div>
    <!-- table表格 -->
    <div>
      <el-table
        :header-cell-style="{ background: '#fafafa' }"
        ref="multipleTableRef"
        :data="tableData"
        style="width: 100%"
      >
        <el-table-column type="selection" width="55" />
        <el-table-column type="index" width="100" label="序号" />
        <el-table-column width="180" prop="date" label="申请时间" />
        <el-table-column width="120" prop="name" label="申请人" />
        <el-table-column label="物品列表" width="120">
          <template #default="{ row }">
            <el-button type="text">详情</el-button>
          </template>
        </el-table-column>
        <el-table-column prop="channel" label="采购渠道" width="120" />
        <el-table-column prop="illustrate" label="申请说明" width="270" />
        <el-table-column prop="state" label="状态" width="120" />
        <el-table-column prop="illustrate" label="操作">
          <template #default="{ row }">
            <el-button type="text">编辑</el-button>
            <el-button type="text">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <!-- 资产新增页面 -->
    <addPurchaseVue :addData="addData" @closeAddDialog="closeAddDialog" />
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import addPurchaseVue from './addPurchase.vue'
const addPurch = () => {
  // 给新增传递的数据
  const addData = reactive({
    showAddDialog: false
  })
  // 打开新增
  const addAssets = () => {
    addData.showAddDialog = true
  }
  const closeAddDialog = () => {
    addData.showAddDialog = false
  }
  return { addData, closeAddDialog, addAssets }
}

export default defineComponent({
  name: '',
  components: {
    addPurchaseVue
  },
  setup() {
    // 资产采购table表中的筛选
    const formdata = reactive({
      // 筛选方式默认名字
      head: 'name',
      // 筛选的内容
      contant: '',
      // 时间筛选的内容
      dates: [],
      // 筛选渠道的内容
      channel: ''
    })
    // 筛选的方式
    const options1 = [
      {
        value: 'taobao',
        label: '淘宝'
      },
      {
        value: 'jingdong',
        label: '京东'
      }
    ]
    // 筛选的渠道
    const options = [
      {
        value: 'name',
        label: '姓名'
      },
      {
        value: 'times',
        label: '时间范围'
      },
      {
        value: 'channel',
        label: '采购渠道'
      }
    ]
    // table表单内容
    interface User {
      date: string
      name: string
      channel: string
      illustrate: string
      state: string
    }
    const tableData: User[] = [
      {
        date: '2016-05-03',
        name: 'Tom',
        channel: '淘宝',
        illustrate: '因部门迎来多名员工需要采购一批电脑',
        state: '审批中'
      },
      {
        date: '2016-05-02',
        name: 'Tom',
        channel: '淘宝',
        illustrate: '因部门迎来多名员工需要采购一批电脑',
        state: '审批中'
      },
      {
        date: '2016-05-04',
        name: 'Tom',
        channel: '淘宝',
        illustrate: '因部门迎来多名员工需要采购一批电脑',
        state: '审批中'
      },
      {
        date: '2016-05-01',
        name: 'Tom',
        channel: '京东',
        illustrate: '因部门迎来多名员工需要采购一批电脑',
        state: '已驳回'
      },
      {
        date: '2016-05-08',
        name: 'Tom',
        channel: '京东',
        illustrate: '因部门迎来多名员工需要采购一批电脑',
        state: '已驳回'
      },
      {
        date: '2016-05-06',
        name: 'Tom',
        channel: '京东',
        illustrate: '因部门迎来多名员工需要采购一批电脑',
        state: '已通过'
      },
      {
        date: '2016-05-07',
        name: 'Tom',
        channel: '京东',
        illustrate: '因部门迎来多名员工需要采购一批电脑',
        state: '已通过'
      }
    ]
    return { ...addPurch(), formdata, options, options1, tableData }
  }
})
</script>
<style lang="postcss" scoped>
.assetsa-assetProcurement-components-purchaseTable {
  :deep(.changeType) {
    .firstSelect {
      .el-input__inner {
        width: 200px;
      }
    }
    .el-input__inner {
      width: 300px;
    }
  }
}
</style>
