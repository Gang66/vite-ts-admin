<template>
  <el-dialog
    v-model="data.dialogVisible"
    width="840px"
    custom-class="InnDialog"
    @closed="closeDialog(ruleFormRef)"
    @open="openDialog"
  >
    {{ data.userInfo }}
    <!-- 培训调研 -->
    <el-tabs v-model="fromInfo.number">
      <el-tab-pane label="培训调研" name="1">
        <template #label>
          <span class="text-2xl text-white">培训调研</span>
        </template>

        <el-form
          ref="ruleFormRef"
          :model="inndata"
          :rules="rules"
          v-if="fromInfo.number === '1'"
        >
          <div class="pl-10 pr-10 mt-10">
            <h4 class="font-black">1.您需要什么样的培训内容</h4>
            <el-form-item prop="needs">
              <el-input
                placeholder="请输入创新举措"
                :rows="3"
                v-model="inndata.needs"
                type="textarea"
              ></el-input
            ></el-form-item>
          </div>
          <div class="pl-10 pr-10 mt-3">
            <h4 class="font-black">2.您需要什么样的培训方式，如何调整为妥</h4>

            <el-form-item prop="trainingMethod">
              <el-input
                placeholder="请输入创新举措"
                :rows="3"
                v-model="inndata.trainingMethod"
                type="textarea"
              ></el-input
            ></el-form-item>
          </div>
          <div class="pl-10 pr-10 mt-3">
            <h4 class="font-black">
              3.您需要对培训时间、培训试题、培训课程数量与质量有何建议
            </h4>

            <el-form-item prop="trainingSuggest">
              <el-input
                placeholder="请输入创新举措"
                :rows="3"
                v-model="inndata.trainingSuggest"
                type="textarea"
              ></el-input
            ></el-form-item>
          </div>
        </el-form>
      </el-tab-pane>
      <el-tab-pane label="意见建议" name="2">
        <template #label>
          <span class="text-2xl text-white">意见培训</span>
        </template>
        <div class="pl-10 pr-10 mt-10" v-if="fromInfo.number === '2'">
          <h4 class="font-black">
            1.您对公司在发展过程中存在哪些问题以及有何建议
          </h4>
          <el-form ref="ruleFormRef" :model="inndata" :rules="rules">
            <el-form-item prop="opinionTraining">
              <el-input
                placeholder="请输入创新举措"
                :rows="6"
                v-model="inndata.opinionTraining"
                type="textarea"
              ></el-input
            ></el-form-item>
          </el-form>
        </div>
      </el-tab-pane>
      <el-tab-pane label="创新举措" name="3">
        <template #label>
          <span class="text-2xl text-white">创新举措</span>
        </template>
        <div class="pl-10 pr-10 mt-10" v-if="fromInfo.number === '3'">
          <h4 class="font-black">
            1.您对本职工作或其他岗位工作有何改善、改进措施，得以提升工作品质、效率、效果、或减少工作投入
          </h4>
          <el-form ref="ruleFormRef" :model="inndata" :rules="rules">
            <el-form-item prop="innovativeInitiatives">
              <el-input
                placeholder="请输入创新举措"
                :rows="6"
                v-model="inndata.innovativeInitiatives"
                type="textarea"
              ></el-input
            ></el-form-item>
          </el-form>
        </div>
      </el-tab-pane>
      <el-tab-pane label="其他建议" name="4">
        <template #label>
          <span class="text-2xl text-white">其他建议</span>
        </template>
        <div class="pl-10 pr-10 mt-10" v-if="fromInfo.number === '4'">
          <h4 class="font-black">
            1.您对公司的发展、经营、管理、销售、机制、流程等方面还有什么建议
          </h4>
          <el-form ref="ruleFormRef" :model="inndata" :rules="rules">
            <el-form-item prop="otherSuggestion">
              <el-input
                placeholder="请输入创新举措"
                :rows="6"
                v-model="inndata.otherSuggestion"
                type="textarea"
              ></el-input></el-form-item
          ></el-form>
        </div>
      </el-tab-pane>
      <div class="pl-10 pr-10 mt-3 flex items-center">
        <el-checkbox v-model="inndata.checked1" label="匿名" size="large" />
        <span class="ml-2 mt-1 text-orange-200"
          >勾选后，表示用户可匿名参与此次问卷调查</span
        >
      </div>
    </el-tabs>
    <template #footer>
      <div class="flex justify-center">
        <el-button size="large" @click="closeDialog(ruleFormRef)"
          >取消</el-button
        >
        <el-button size="large" type="primary" @click="confirm(ruleFormRef)"
          >提交</el-button
        >
      </div>
    </template>
  </el-dialog>
</template>
<script lang="ts">
import { defineComponent, reactive, ref, SetupContext } from 'vue'
import type { FormInstance, FormRules } from 'element-plus'
const inndatademo = {
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
  // 是否匿名
  checked1: false
}

const one = (data: any) => {
  const ruleFormRef = ref<FormInstance>()
  const rules = reactive({
    needs: [
      {
        required: true,
        message: '必填项',
        trigger: 'blur'
      }
    ],
    trainingMethod: [{ required: true, message: '必填项', trigger: 'blur' }],
    trainingSuggest: [{ required: true, message: '必填项', trigger: 'blur' }],
    opinionTraining: [{ required: true, message: '必填项', trigger: 'blur' }],
    otherSuggestion: [{ required: true, message: '必填项', trigger: 'blur' }],
    innovativeInitiatives: [
      { required: true, message: '必填项', trigger: 'blur' }
    ]
  })
  // tab页显示第一个
  const activeName = ref('1')
  const inndata = ref()
  inndata.value = JSON.parse(JSON.stringify(inndatademo))

  inndata.value = data.fromInfo.value
  // 关闭dialog
  const closeDialog = (formEl: FormInstance | undefined) => {
    data.SetupContext.emit('closed')
    formEl.resetFields()
    inndata.value = JSON.parse(JSON.stringify(inndatademo))
  }
  // 提交dialog
  const confirm = async (formEl: FormInstance | undefined) => {
    if (!formEl) return
    await formEl.validate((valid: any, fields: any) => {
      if (valid) {
        console.log(inndata.value)

        console.log('submit!')
      } else {
        console.log('error submit!', fields)
      }
    })
    // closeDialog()
  }

  return {
    rules,
    ruleFormRef,
    closeDialog,
    inndata,
    activeName,
    confirm
  }
}

export default defineComponent({
  name: '',
  props: {
    data: {
      type: Object
    }
  },

  setup(props, SetupContext) {
    const fromInfo = ref()
    fromInfo.value = props.data.userInfo
    const openDialog = () => {
      fromInfo.value = props.data.userInfo
    }
    return {
      fromInfo,
      openDialog,
      ...one({ SetupContext, fromInfo })
    }
  }
})
</script>
<style>
.el-dialog__header {
  display: none;
}
.InnDialog {
  background-color: #9ebbf8;
  border-radius: 20px;
}
</style>
