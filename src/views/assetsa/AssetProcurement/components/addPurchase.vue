<template>
  <div class="assetsa-AssetProcurement-components-addPurchase">
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
                <el-input disabled v-model="ruleForm.department1"></el-input>
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
          <span class="text-blue-400 cursor-pointer" @click="addthing"
            >+添加</span
          >
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
          <el-table-column prop="name" label="物品名称" width="150">
            <template #default="{ row, $index }">
              <div
                class="h-5 w-full"
                v-if="showType[$index].name"
                @click="inputF('name', $index)"
              >
                {{ row.name }}
              </div>
              <el-input
                placeholder="请输入物品名称"
                v-focus
                v-model="row.name"
                v-else
                @blur="blurBtn('name', $index)"
              ></el-input>
            </template>
          </el-table-column>
          <el-table-column prop="Specification" label="规格型号" width="150">
            <template #default="{ row, $index }">
              <div
                class="h-5 w-full"
                v-if="showType[$index].Specification"
                @click="inputF('Specification', $index)"
              >
                {{ row.Specification }}
              </div>
              <el-input
                placeholder="请输入规格型号"
                v-focus
                v-model="row.Specification"
                v-else
                @blur="blurBtn('Specification', $index)"
              ></el-input>
            </template>
          </el-table-column>

          <el-table-column prop="unit" label="计量单位" width="150">
            <template #default="{ row, $index }">
              <div
                class="h-5 w-full"
                v-if="showType[$index].unit"
                @click="inputF('unit', $index)"
              >
                {{ row.unit }}
              </div>
              <el-input
                placeholder="请输入计量单位"
                v-focus
                v-model="row.unit"
                v-else
                @blur="blurBtn('unit', $index)"
              ></el-input>
            </template>
          </el-table-column>
          <el-table-column property="unitPrice" label="单价" width="150">
            <template #default="{ row, $index }">
              <div
                class="h-5 w-full"
                v-if="showType[$index].unitPrice"
                @click="inputF('unitPrice', $index)"
              >
                {{ row.unitPrice }}
              </div>
              <el-input
                placeholder="请输入单价"
                oninput="value=value.replace(/^\.+|[^\d.]/g,'').replace(/^0{1,}/g,'')"
                v-focus
                v-model="row.unitPrice"
                v-else
                @blur="blurBtn('unitPrice', $index)"
              ></el-input>
            </template>
          </el-table-column>
          <el-table-column property="quantity" label="申请数量" width="150">
            <template #default="{ row, $index }">
              <div
                class="w-full h-5"
                v-focus
                v-if="showType[$index].quantity"
                @click="inputF('quantity', $index)"
              >
                {{ row.quantity }}
              </div>
              <el-input
                placeholder="请输入数量"
                oninput="value=value.replace(/^\.+|[^\d.]/g,'').replace(/^0{1,}/g,'')"
                v-focus
                v-model="row.quantity"
                v-else
                @blur="blurBtn('quantity', $index)"
              ></el-input>
            </template>
          </el-table-column>
          <el-table-column label="预计费用" width="150">
            <template #default="{ row, column }">
              <div>{{ row.unitPrice * row.quantity }}</div>
            </template>
          </el-table-column>
          <el-table-column label="备注">
            <template #default="{ row, $index }">
              <div
                class="h-5 w-full"
                v-if="showType[$index].Remark"
                @click="inputF('Remark', $index)"
              >
                {{ row.Remark }}
              </div>
              <el-input
                placeholder="请输入备注"
                v-focus
                v-model="row.Remark"
                v-else
                @blur="blurBtn('Remark', $index)"
              ></el-input>
            </template>
          </el-table-column>
        </el-table>
      </div>
      <div
        class="w-full h-10 bg-slate-100 flex justify-end items-center pr-4 text-xs"
      >
        <span>预计总金额(元) </span>
      </div>
      <template #footer>
        <span class="dialog-footer">
          <el-button @click="Cancel(ruleFormRef)">取消</el-button>
          <el-button type="primary" @click="Confirm(ruleFormRef)"
            >提交</el-button
          >
        </span>
      </template>
    </el-dialog>
  </div>
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
      let month: any = date.getMonth() + 1
      month = month < 10 ? '0' + month : month
      let strdate: any = date.getDate()
      strdate = strdate < 10 ? '0' + strdate : strdate
      let hour: any = date.getHours()
      hour = hour < 10 ? '0' + hour : hour
      let min: any = date.getMinutes()
      min = min < 10 ? '0' + min : min
      let currentDate =
        year + '-' + month + '-' + strdate + ' ' + hour + ':' + min
      return currentDate
    }

    // 表单的数据
    const ruleFormdemo = {
      times: '',
      name: '测试人',
      department: '测试事业部',
      department1: '测试部门',
      channel: '',
      illustrate: '',
      tableData: []
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

    //添加
    const addthing = () => {
      var obj = {
        name: '',
        Specification: '',
        unit: '',
        unitPrice: 0,
        quantity: 0,
        totalMoney: null,
        Remark: ''
      }
      ruleForm.value.tableData.push(obj)
      showType.push({
        name: false,
        Specification: true,
        unit: true,
        unitPrice: true,
        quantity: true,
        Remark: true
      })
    }
    // 控制是否显示input框或者span
    const showType: any = reactive([
      {
        name: false,
        Specification: true,
        unit: true,
        unitPrice: true,
        quantity: true,
        Remark: true
      }
    ])
    //span 点击事件
    const inputF = (val: any, index: number) => {
      showType[index][val] = false
    }
    //input blur 失去焦点出现span
    const blurBtn = (val: any, index: number) => {
      showType[index][val] = true
    }
    return {
      openDialog,
      Cancel,
      ruleForm,
      ruleFormRef,
      rules,
      Confirm,
      options,
      getCurrentTime,
      addthing,
      showType,
      inputF,
      blurBtn
    }
  }
})
</script>
<style lang="postcss" scoped>
.assetsa-AssetProcurement-components-addPurchase {
  :deep(.el-table--fit) {
  }
}
</style>
