<template>
  <el-dialog
    v-model="addData.showAddDialog"
    width="70%"
    @closed="Cancel(ruleFormRef)"
    @opened="openDialog(ruleFormRef)"
  >
    <h2 class="text-lg font-bold">新增资产采购</h2>
    <hr class="mt-4 mb-4" />
    <!-- 表单内容 -->
    <div>
      <el-form
        ref="ruleFormRef"
        :model="ruleForm"
        :rules="rules"
        class="demo-ruleForm"
        status-icon
        label-width="80px"
      >
        <h2 class="font-extrabold mb-2">基础信息</h2>
        <el-row>
          <el-col :span="8">
            <el-form-item label="申请时间">
              <el-input v-model="ruleForm.times" disabled></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="申请人">
              <el-input v-model="ruleForm.name" disabled></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="事业部">
              <el-input v-model="ruleForm.department" disabled></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="8">
            <el-form-item label="部门" prop="department1">
              <el-input v-model="ruleForm.department1"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="采购渠道" prop="channel">
              <el-select v-model="ruleForm.channel" style="width: 230px">
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                />
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="申请说明" prop="illustrate">
              <el-input v-model="ruleForm.illustrate"> </el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
    </div>
    <!-- table表格内容 -->
    <div>
      <div class="flex justify-between">
        <h2 class="font-extrabold mb-2">申请明细-物品列表</h2>
        <span class="text-blue-400">+添加</span>
      </div>
      <el-table
        border
        :data="ruleForm.tableData"
        style="width: 100%"
        :header-cell-style="{
          backgroundColor: '#fafafa'
        }"
      >
        <el-table-column type="selection" width="55" />
        <el-table-column prop="name" label="物品名称" width="150" />
        <el-table-column
          property="Specification"
          label="规格型号"
          width="150"
        />

        <el-table-column prop="unit" label="计量单位" width="150">
        </el-table-column>
        <el-table-column property="unitPrice" label="单价" width="150" />
        <el-table-column property="quantity" label="申请数量" width="150" />
        <el-table-column label="预计费用" width="150">
          <template #default="{ row }">
            {{ row.unitPrice * row.quantity }}
          </template>
        </el-table-column>
        <el-table-column label="备注">
          <template #default="{ row }"></template>
        </el-table-column>
      </el-table>
    </div>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="Cancel(ruleFormRef)">取消</el-button>
        <el-button type="primary" @click="Confirm(ruleFormRef)">提交</el-button>
      </span>
    </template>
  </el-dialog>
</template>
<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
export default defineComponent({
  name: '',
  props: {
    addData: {
      type: Object
    }
  },
  emits: ['closeAddDialog'],
  setup(prop, ctx) {
    // 获取当前时间
    const getCurrentTime = () => {
      let date = new Date()
      let year = date.getFullYear()
      let month = date.getMonth() + 1
      month < 10 ? '0' + month : month
      let strdate = date.getDate()
      strdate < 10 ? '0' + strdate : strdate
      let hour = date.getHours()
      hour < 10 ? '0' + hour : hour
      let min = date.getMinutes()
      min < 10 ? '0' + min : min
      let currentDate =
        year + '-' + month + '-' + strdate + ' ' + hour + ':' + min
      return currentDate
    }

    // 表单的数据
    const ruleFormdemo = {
      times: '',
      name: '测试人',
      department: '测试部门',
      department1: '',
      channel: '',
      illustrate: '',
      tableData: [
        {
          show: [0, 0, 0, 0, 0],
          id: 1,
          name: '人体工学椅',
          Specification: '#3022',
          unit: '个',
          unitPrice: 2400,
          quantity: 26,
          totalMoney: null
        }
      ]
    }
    const ruleForm = ref()
    ruleForm.value = JSON.parse(JSON.stringify(ruleFormdemo))
    const ruleFormRef = ref()
    // 表单校验
    const rules = reactive({
      department1: [
        {
          required: true,
          message: '请输入所在部门',
          trigger: 'blur'
        }
      ],
      channel: [
        {
          required: true,
          message: '请选择采购渠道',
          trigger: 'blur'
        }
      ],
      illustrate: [
        {
          required: true,
          message: '请输入申请说明',
          trigger: 'blur'
        }
      ]
    })
    // 采购渠道下拉框的内容
    const options = [
      {
        value: 'taobao',
        label: '淘宝'
      },
      {
        value: 'jingdong',
        label: '京东'
      }
    ]

    // 打开dialog的时候自动获取当前时间
    const openDialog = () => {
      ruleForm.value.times = getCurrentTime()
    }

    // 控制进入table表单后点击出现输入框
    // const editdes = ref(null)
    // const switchDesState = (row: any) => {
    //   editdes.value = row.id
    // }
    // const levelDesIt = (row: any) => {
    //   editdes.value = null
    // }

    //   点击取消按钮
    const Cancel = (val: any) => {
      val.resetFields()
      ruleForm.value = JSON.parse(JSON.stringify(ruleFormdemo))
      ctx.emit('closeAddDialog')
    }
    // 点击提交
    const Confirm = async (formEl: any) => {
      if (!formEl) return
      await formEl.validate((valid: any, fields: any) => {
        if (valid) {
          console.log('submit!')
        } else {
          console.log('error submit!', fields)
        }
      })
    }
    return {
      // editdes,
      // switchDesState,
      // levelDesIt,
      openDialog,
      Cancel,
      ruleForm,
      ruleFormRef,
      rules,
      Confirm,
      options,
      getCurrentTime
    }
  }
})
</script>
<style scoped></style>
