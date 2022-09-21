<template>
  <div class="chilDialog">
    <el-dialog
      v-model="childata.isOpen"
      width="400px "
      @closed="closed(ruleFormRef)"
      @opened="opened(ruleFormRef)"
    >
      <!-- 头部 -->
      <div
        class="bg-blue-600 w-full h-10 flex justify-between items-center pl-2"
      >
        <h2 class="text-white">添加工作内容</h2>
        <div class="mr-1 flex items-center">
          <div>
            <el-button size="mini" type="primary" @click="Confirm(ruleFormRef)"
              >提交</el-button
            >
          </div>
          <div
            class="h-5 w-5 bg-slate-300 ml-2 rounded-full flex items-center justify-center"
            @click="close"
          >
            <span class="text-lg text-white cursor-pointer">×</span>
          </div>
        </div>
      </div>
      <!-- 时间的内容 -->
      <div class="p-4 w-full" v-if="childata.showTime < 10">
        <!-- 日期 -->
        <div class="flex">
          <span>工作日期</span>
          <span class="ml-2 font-extrabold">{{ NowTime }}</span>
        </div>
        <!-- 时间 -->
        <div class="flex items-center mt-6">
          <div>
            <span>工作时间</span>
          </div>
          <div class="unline w-200 flex items-center ml-2">
            <span>{{ whenTime }}</span>
            <span class="ml-1"
              ><el-input
                @input="inputed"
                placeholder="0"
                type="number"
                v-model="data.start"
              ></el-input
            ></span>
            <span>分至</span>
            <span class="ml-1"
              ><el-input
                @input="inputed1"
                :min="0"
                :max="59"
                placeholder="0"
                type="number"
                v-model="data.end"
              ></el-input
            ></span>
            <span>分</span>
          </div>
        </div>
        <!-- 内容 -->
        <div class="w-200 flex items-center mt-6">
          <span>工作内容</span>
          <span class="ml-1 contants">
            <el-form
              ref="ruleFormRef"
              :model="data"
              :rules="rules"
              :size="formSize"
              status-icon
            >
              <el-form-item prop="contant">
                <el-input
                  v-model="data.contant"
                  placeholder="请输入工作内容"
                ></el-input></el-form-item
            ></el-form>
          </span>
        </div>
      </div>
      <!-- 今日总结的内容 -->
      <div class="p-4 w-full" v-if="childata.showTime > 10">
        <div class="flex items-center">
          <span>工作内容</span>
          <span class="ml-4 textcss">
            <el-form
              ref="ruleFormRef"
              :model="data"
              :rules="rules"
              :size="formSize"
              status-icon
            >
              <el-form-item prop="contant1">
                <el-input type="textarea" v-model="data.contant1"> </el-input>
              </el-form-item>
            </el-form>
          </span>
        </div>
        <div>
          <span>自我评定</span>
          <span>
            <el-radio-group v-model="radio1" class="ml-4">
              <el-radio label="好" size="large">好</el-radio>
              <el-radio label="中" size="large">中</el-radio>
              <el-radio label="差" size="large">差</el-radio>
            </el-radio-group></span
          >
        </div>
      </div>
    </el-dialog>
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, ref, SetupContext } from 'vue'
import type { FormInstance, FormRules } from 'element-plus'
import { ElMessage } from 'element-plus'
export default defineComponent({
  name: '',
  props: {
    childata: {
      type: Object
    }
  },
  emits: ['closed'],
  setup(prop, SetupContext) {
    //   点开今日数据后显示哪一个时间段 如：08:00
    const whenTime = ref('')
    const opened = () => {
      if (prop.childata.showTime === 1) {
        whenTime.value = '08时'
      } else if (prop.childata.showTime === 2) {
        whenTime.value = '09时'
      } else if (prop.childata.showTime === 3) {
        whenTime.value = '10时'
      } else if (prop.childata.showTime === 4) {
        whenTime.value = '11时'
      } else if (prop.childata.showTime === 5) {
        whenTime.value = '13时'
      } else if (prop.childata.showTime === 6) {
        whenTime.value = '14时'
      } else if (prop.childata.showTime === 7) {
        whenTime.value = '15时'
      } else if (prop.childata.showTime === 8) {
        whenTime.value = '16时'
      } else if (prop.childata.showTime === 9) {
        whenTime.value = '17时'
      }
    }
    //   开始时间小于59 大于0
    const inputed = (val: any) => {
      data.start = val.replace(/[^\d]/g, '').replace(/^0{1,}/g, '')
      if (val < 0) {
        data.start = 0
      }
      if (val > 59) {
        data.start = 59
      }
    }
    // 现在的年月日
    const NowTime = ref()
    const GetTime = () => {
      let nowData = new Date()
      let yy = nowData.getFullYear()
      let mm = nowData.getMonth() + 1
      let dd = nowData.getDate()
      NowTime.value = yy + '年' + mm + '月' + dd + '日'
    }
    GetTime()
    //   结束时间小于59 大于0
    const inputed1 = (val: any) => {
      data.end = val.replace(/[^\d]/g, '').replace(/^0{1,}/g, '')

      if (val < 0) {
        data.end = 0
      }
      if (val > 59) {
        data.end = 59
      }
    }
    const ruleFormRef = ref<FormInstance>()
    const rules = reactive<FormRules>({
      contant: [
        {
          required: true,
          message: '请输入备注',
          trigger: 'blur'
        }
      ],
      contant1: [
        {
          required: true,
          message: '请输入工作内容',
          trigger: 'blur'
        }
      ]
    })
    const radio1 = ref('')
    // 提交表单
    const Confirm = async (formEl: FormInstance | undefined) => {
      if (!formEl) return
      await formEl.validate((valid: any, fields: any) => {
        if (valid && data.end > data.start) {
          console.log('submit!')
        } else {
          if (data.end <= data.start) {
            ElMessage.error({
              message: '结束时间必须大于开始时间',
              center: true
            })
          }
          console.log('error submit!', fields)
        }
      })
    }
    // 表单数据
    const data = reactive({
      start: 0,
      end: 0,
      contant: '',
      contant1: ''
    })
    const closed = (val: any) => {
      data.start = 0
      data.end = 0
      val.resetFields()
    }
    const close = () => {
      SetupContext.emit('closed')
    }
    return {
      NowTime,
      opened,
      whenTime,
      close,
      data,
      radio1,
      ruleFormRef,
      rules,
      closed,
      inputed,
      inputed1,
      Confirm
    }
  }
})
</script>
<style lang="postcss" scoped>
.chilDialog {
  .textcss {
    :deep(.el-textarea__inner) {
      width: 250px;
    }
  }
  .contants {
    :deep(.el-input__inner) {
      width: 200px;
    }
  }
  :deep(.el-input__inner) {
    width: 60px;
    border-top-width: 0px;
    border-left-width: 0px;
    border-right-width: 0px;
    border-bottom-width: 1px;
  }
  :deep(.el-dialog__body) {
    padding: 0;
  }
}
</style>
