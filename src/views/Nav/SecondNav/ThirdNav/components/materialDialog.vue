<template>
  <div class="Nav-SecondNav-components-materiaDialog">
    <el-dialog
      v-model="data.dialogVisible"
      width="850px"
      @closed="Cancel(ruleFormRef)"
    >
      <!-- 头部 -->
      <div
        class="bg-blue-600 w-full h-10 flex justify-between items-center pl-2"
      >
        <h2 class="text-white">上传素材</h2>
        <div class="mr-1 flex items-center">
          <div
            class="h-5 w-5 bg-slate-300 ml-2 rounded-full flex items-center justify-center"
            @click="Cancel(ruleFormRef)"
          >
            <span class="text-lg text-white cursor-pointer">×</span>
          </div>
        </div>
      </div>
      <!-- 内容 -->
      <div class="p-3">
        <!-- 基础信息 -->
        <div>
          <!-- 基础信息头部 -->
          <div class="flex justify-between">
            <div class="flex items-center">
              <div class="w-1 h-4 bg-blue-400"></div>
              <div class="font-black ml-3 text-lg">基础信息</div>
            </div>
            <div>
              <span>新人训课程 <el-switch v-model="formdata.value1" /></span>
            </div>
          </div>
          <!-- 基础信息内容 -->
          <div class="mt-2">
            <el-form
              :model="formdata"
              label-width="80px"
              ref="ruleFormRef"
              :rules="rules"
            >
              <el-row>
                <el-col :span="5">
                  <el-form-item label="课件名称" prop="name">
                    <el-input
                      v-model="formdata.name"
                      placeholder="请选择"
                    ></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="培训需求" prop="need">
                    <el-select
                      v-model="formdata.need"
                      placeholder="请选择"
                    ></el-select>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="课件等级" prop="grade">
                    <el-select
                      v-model="formdata.grade"
                      placeholder="请选择"
                    ></el-select>
                  </el-form-item>
                </el-col>
                <el-col :span="6">
                  <el-form-item label="课件类型" prop="type">
                    <el-select
                      v-model="formdata.type"
                      placeholder="请选择"
                    ></el-select>
                  </el-form-item>
                </el-col>
              </el-row>
              <el-row>
                <el-col :span="6">
                  <el-form-item label="学习时长">
                    <div class="addbtn flex">
                      <el-button
                        @click="toggle(-1)"
                        :disabled="formdata.duration === 1"
                        >-
                      </el-button>
                      <el-input
                        v-model="formdata.duration"
                        onkeyup="value=value.replace(/[^\d]/g,'')"
                      />
                      <el-button @click="toggle(1)">+</el-button>
                    </div>
                  </el-form-item>
                </el-col>
                <el-col :span="7">
                  <el-form-item label="面向人员" prop="personnel">
                    <el-select
                      v-model="formdata.personnel"
                      placeholder="请选择"
                    ></el-select>
                  </el-form-item>
                </el-col>
                <el-col :span="10">
                  <el-form-item label="课件说明" prop="illustrate">
                    <el-input
                      v-model="formdata.illustrate"
                      placeholder="请输入"
                    ></el-input>
                  </el-form-item>
                </el-col>
              </el-row>
              <el-row>
                <el-col :span="23">
                  <div class="flex justify-end w-full">
                    <el-button
                      type="primary"
                      style="margin-right: 10px"
                      @click="openChilDialog"
                      >上传素材封面</el-button
                    >
                    <el-upload
                      ref="upload"
                      class="upload-demo"
                      action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15"
                      :limit="1"
                      :on-exceed="handleExceed"
                      :auto-upload="false"
                    >
                      <template #trigger class="mr-3">
                        <el-button type="primary">新增</el-button>
                      </template>
                      <el-button
                        style="margin-left: 10px"
                        class="ml-3"
                        type="success"
                        @click="submitUpload"
                      >
                        上传
                      </el-button>
                    </el-upload>
                  </div>
                </el-col>
              </el-row>
            </el-form>
          </div>
        </div>
        <!-- 课件内容 -->
        <div>
          <!-- 基础信息头部 -->
          <div class="flex justify-between">
            <div class="flex items-center">
              <div class="w-1 h-4 bg-blue-400"></div>
              <div class="font-black ml-3 text-lg">课件内容</div>
            </div>
          </div>
          <!-- 内容 -->
          <div class="tablechange">
            <el-table
              border
              :data="tableData"
              style="width: 100%"
              :header-cell-style="{
                'font-size': '12px',
                padding: '0px',
                background: '#E7F4FE',
                color: '#303133',
                height: '24px',
                textAlign: 'center',
                fontWeight: '500'
              }"
              :cell-style="{
                textAlign: 'center',
                color: '#333',
                height: '24px',
                padding: '0px'
              }"
            >
              <el-table-column type="index" label="序号" width="120" />
              <el-table-column prop="name" label="文件名" width="200" />
              <el-table-column prop="size" label="大小" width="200" />
              <el-table-column prop="size" label="状态" width="200" />
              <el-table-column prop="size" label="操作" />
            </el-table>
          </div>
        </div>
      </div>
      <template #footer>
        <span class="dialog-footer flex justify-center">
          <el-button @click="Cancel(ruleFormRef)">取消</el-button>
          <el-button type="primary" @click="Confirm(ruleFormRef)"
            >提交</el-button
          >
        </span>
      </template>
    </el-dialog>
    <childDialogVue :childata="childata" @closeChildDialog="closeChildDialog" />
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import childDialogVue from './childDialog.vue'
import type {
  FormInstance,
  FormRules,
  UploadInstance,
  UploadProps,
  UploadRawFile
} from 'element-plus'

const putChildDialog = () => {
  const closeChildDialog = () => {
    childata.showChildDialog = false
  }
  const childata = reactive({
    showChildDialog: false
  })
  const openChilDialog = () => {
    childata.showChildDialog = true
  }
  return { childata, openChilDialog, closeChildDialog }
}
export default defineComponent({
  name: '',
  components: {
    childDialogVue
  },
  props: {
    data: {
      type: Object
    }
  },
  emits: ['closematerial'],
  setup(prop, context) {
    // 关闭dialog弹窗
    const Cancel = (val: any) => {
      val.resetFields()
      formdata.value = JSON.parse(JSON.stringify(formdatademo))
      context.emit('closematerial')
    }
    // 表单数据
    const formdatademo = {
      // switch的切换
      value1: false,
      name: '',
      need: '',
      grade: '',
      type: '',
      duration: 1,
      personnel: '',
      illustrate: ''
    }
    // 清空表单
    const formdata = ref()
    formdata.value = JSON.parse(JSON.stringify(formdatademo))

    // 增加减少学习时长
    const toggle = (val: any) => {
      formdata.value.duration = Number(formdata.value.duration) + val
    }
    // 表单校验
    const ruleFormRef = ref<FormInstance>()
    // 点击提交表单
    const Confirm = async (formEl: FormInstance | undefined) => {
      if (!formEl) return
      await formEl.validate((valid: any, fields: any) => {
        if (valid) {
          console.log('submit!')
        } else {
          console.log('error submit!', fields)
        }
      })
    }
    // 表单验证规则
    const rules = reactive<FormRules>({
      name: [
        {
          required: true,
          message: '必填项',
          trigger: 'blur'
        }
      ],
      need: [
        {
          required: true,
          message: '必填项',
          trigger: 'blur'
        }
      ],
      grade: [
        {
          required: true,
          message: '必填项',
          trigger: 'blur'
        }
      ],
      type: [
        {
          required: true,
          message: '必填项',
          trigger: 'blur'
        }
      ],
      personnel: [
        {
          required: true,
          message: '必填项',
          trigger: 'blur'
        }
      ],
      illustrate: [
        {
          required: true,
          message: '必填项',
          trigger: 'blur'
        }
      ]
    })

    // 提交上传文件的代码
    const upload = ref<UploadInstance>()
    const handleExceed: UploadProps['onExceed'] = (files: any) => {
      upload.value!.clearFiles()
      const file = files[0] as UploadRawFile
      upload.value!.handleStart(file)
    }

    const submitUpload = () => {
      upload.value!.submit()
    }

    // table的数据

    const tableData = null

    return {
      tableData,
      ...putChildDialog(),
      Cancel,
      formdata,
      toggle,
      ruleFormRef,
      rules,
      Confirm,
      upload,
      handleExceed,
      submitUpload
    }
  }
})
</script>
<style lang="postcss" scoped>
.Nav-SecondNav-components-materiaDialog {
  .tablechange {
    :deep(.el-table__header) {
      background-color: #e7f4fe;
    }
  }
  .addbtn {
    :deep(.el-button) {
      background-color: #f5f7fa;
    }
  }
  :deep(.el-dialog__body) {
    padding: 0;
  }
}
</style>
