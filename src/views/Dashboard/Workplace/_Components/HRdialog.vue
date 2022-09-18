<template>
  <el-dialog
    v-model="data.isDialog"
    :title="data.title"
    width="820px"
    custom-class="dialogHeader"
    @closed="Close(ruleFormRef)"
  >
    <!-- 面试者信息 -->
    <el-form :model="form" label-width="110px" ref="ruleFormRef" :rules="rules">
      <el-row>
        <el-col :span="24">
          <div class="flex items-center">
            <div class="w-1 h-4 bg-purple-300"></div>
            <div class="font-black ml-3">面试者信息</div>
          </div>
        </el-col>
      </el-row>
      <!-- 面试者信息内容 -->
      <div style="border: 2px dotted #b3bad7" class="mt-2">
        <el-row>
          <el-col :span="4">
            <div>
              <img src="../../../../assets/img/headerlogo.png" alt="" />
            </div>
          </el-col>

          <el-col :span="16">
            <el-row class="mt-2">
              <el-col :span="8"
                ><div>
                  姓名： <span class="font-black">{{ data.obj.name }}</span>
                </div></el-col
              >
              <el-col :span="8"
                ><div>
                  应聘岗位：
                  <span class="font-black">{{ data.obj.gangwei }}</span>
                </div></el-col
              >
              <el-col :span="8"
                ><div>
                  事业部：
                  <span class="font-black">{{ data.obj.shiyebu }}</span>
                </div></el-col
              >
            </el-row>
            <el-row class="mt-2">
              <el-col :span="8"
                ><div>
                  部门： <span class="font-black">{{ data.obj.bumen }}</span>
                </div></el-col
              >
              <el-col :span="8"
                ><div>
                  面试官：
                  <span class="font-black">{{ data.obj.mianshiguan }}</span>
                </div></el-col
              >
              <el-col :span="8"
                ><div>
                  日期： <span class="font-black">{{ data.obj.riqi }}</span>
                </div></el-col
              >
            </el-row>
          </el-col>
          <el-col :span="4">
            <div class="ml-8">
              <img src="../../../../assets/img/rightlogo.png" alt="" />
            </div>
          </el-col>
        </el-row>
      </div>
      <!-- HR评分 -->
      <el-row>
        <el-col :span="24">
          <div class="flex items-center mt-3">
            <div class="w-1 h-4 bg-purple-300"></div>
            <div class="font-black ml-3">HR评分</div>
            <div class="text-orange-300 ml-1">
              <i>应聘登记表 </i>
              <i class="iconfont icon-a-kuozhanicon_huaban1fuben3"></i>
            </div>
          </div>
        </el-col>
      </el-row>
      <!-- 劳资纠纷 -->
      <el-row>
        <el-col :span="12">
          <el-form-item label="1、劳资纠纷" prop="LaborDispute"
            ><el-radio-group v-model="form.LaborDispute">
              <el-radio label="有" />
              <el-radio label="无" />
            </el-radio-group>
          </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item
            label="2、劳资风险系数"
            label-width="130px"
            prop="laborRisk"
            ><el-radio-group v-model="form.laborRisk">
              <el-radio label="有" />
              <el-radio label="无" />
            </el-radio-group>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 介绍制度 -->
      <el-row>
        <el-col :span="24">
          <el-form-item
            label="3、介绍制度、入职合同、薪酬培新费时态度"
            label-width="305px"
            prop="system"
          >
            <el-radio-group v-model="form.system">
              <el-radio label="理解" />
              <el-radio label="不理解" />
            </el-radio-group>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 整体印象 -->
      <el-row>
        <el-col>
          <el-form-item label="4、整体印象" prop="impression">
            <el-radio-group v-model="form.impression">
              <el-radio label="不优秀" />
              <el-radio label="犹豫使用" />
              <el-radio label="相对优秀" />
              <el-radio label="非常优秀" />
            </el-radio-group>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 建议薪酬 -->
      <el-row>
        <el-col :span="24">
          <el-form-item label="5、建议薪酬"> </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="7">
          <el-form-item label="薪酬类型" prop="typeRemuneration">
            <el-select v-model="form.typeRemuneration" placeholder="正常薪酬">
              <el-option label="1000" value="1000" />
              <el-option label="2000" value="2000" />
            </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="14">
          <el-form-item label="薪酬备注" prop="RemuneratioRemarks">
            <el-input
              placeholder="非正常薪酬请填写"
              v-model="form.RemuneratioRemarks"
            ></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <!-- 正式酬薪 -->
      <el-row>
        <el-col :span="7">
          <el-form-item label="正式酬薪" prop="FormalRemuneration">
            <el-input v-model="form.FormalRemuneration" placeholder="请填写">
              <template #suffix>
                <span style="color: black">元</span>
              </template>
            </el-input>
          </el-form-item>
        </el-col>
        <el-col :span="7">
          <el-form-item label="试用酬薪" prop="tryOutFormalRemuneration">
            <el-input
              v-model="form.tryOutFormalRemuneration"
              placeholder="请填写"
            >
              <template #suffix>
                <span style="color: black">元</span>
              </template>
            </el-input>
          </el-form-item>
        </el-col>
        <el-col :span="7">
          <el-form-item label="试用期限" prop="tryOut">
            <el-select v-model="form.tryOut" placeholder="一个月">
              <el-option label="一个月" value="one"></el-option>
              <el-option label="两个月" value="two"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="18">
          <el-form-item label="6、综合评语" prop="Comments">
            <el-input
              v-model="form.Comments"
              type="textarea"
              placeholder="请输入评语"
            />
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
    <template #footer>
      <span class="dialog-footer flex justify-center">
        <el-button
          color="#626aef"
          @click="Close(ruleFormRef)"
          size="large"
          plain
          >取消</el-button
        >
        <el-button
          color="#626aef"
          @click="Confirm(ruleFormRef)"
          size="large"
          class="text-white"
          >提交</el-button
        >

        <el-button
          color="#626aef"
          @click="resetForm(ruleFormRef)"
          size="large"
          class="text-white"
          plain
          >重置</el-button
        >
      </span>
    </template>
  </el-dialog>
</template>
<script lang="ts">
import { defineComponent, ref, SetupContext, reactive } from 'vue'
import type { FormInstance, FormRules } from 'element-plus'
import { ElMessage } from 'element-plus'

const tempObj = {
  // 试用薪酬
  tryOutFormalRemuneration: '',
  // 正式酬薪
  FormalRemuneration: '',
  //劳资风险系数
  laborRisk: '',
  // 制度
  system: '',
  // 整体印象
  impression: '',
  // 酬薪类型
  typeRemuneration: '',
  // 薪酬备注
  RemuneratioRemarks: '',
  // 综合评语
  Comments: '',
  // 劳资纠纷
  LaborDispute: ''
}

const HRform = (data: any) => {
  const ruleFormRef = ref<FormInstance>()
  const rules = ref<FormRules>({
    FormalRemuneration: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    LaborDispute: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    laborRisk: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    system: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    impression: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    typeRemuneration: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    RemuneratioRemarks: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    tryOutFormalRemuneration: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    tryOut: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ]
  })
  // const tryOut = ref()

  const form = ref()
  form.value = JSON.parse(JSON.stringify(tempObj))
  // 关闭按钮
  const Close = (formEl: FormInstance | undefined) => {
    data.context.emit('close')
    formEl.resetFields()
    form.value = JSON.parse(JSON.stringify(tempObj))
  }
  // 提交按钮
  const Confirm = async (formEl: FormInstance | undefined) => {
    if (!formEl) return
    await formEl.validate((valid: any, fields: any) => {
      if (valid) {
        ElMessage({
          showClose: true,
          message: '提交成功',
          type: 'success'
        })
        data.context.emit('close')
      } else {
        ElMessage({
          showClose: true,
          message: '必填项没有填',
          type: 'error'
        })
        // alert('必填项未填')
      }
    })
  }
  // 重置按钮
  const resetForm = (formEl: FormInstance | undefined) => {
    if (!formEl) return
    // formEl.resetFields()
    form.value = JSON.parse(JSON.stringify(tempObj))
    // formEl.resetFields()
  }
  return { Close, Confirm, ruleFormRef, rules, form, resetForm }
}
export default defineComponent({
  name: 'HRdialog',
  props: {
    modelValue: Boolean,
    data: {
      type: Object,
      default: {
        isDialog: false,
        title: '',
        arr: [],
        id: 0,
        obj: {}
      }
    }
  },
  emits: ['close'],
  setup(props, context: SetupContext) {
    return {
      ...HRform({ context })
    }
  }
})
</script>
<style lang="postcss" scoped>
.dialogHeader {
  :deep(.el-dialog__header) {
    background-color: #516bdb;
    color: white;
  }
  :deep(.el-dialog__title) {
    color: white;
  }
}
</style>
