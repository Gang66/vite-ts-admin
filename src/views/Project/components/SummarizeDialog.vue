<template>
  <div class="dialogClass">
    <el-dialog
      v-model="data.dialogVisible"
      width="800px"
      @closed="closedOne(ruleFormRef)"
    >
      <div
        class="w-full bg-blue-400 text-white pl-6"
        style="height: 40px; line-height: 40px"
      >
        工作总结
      </div>
      <!-- 所有内容 -->
      <div class="p-3">
        <!-- 今日数据内容 -->
        <div>
          <!-- 今日数据表头 -->
          <div class="flex justify-between">
            <div class="flex mt-4">
              <div class="w-6 h-6 mt-2">
                <img src="../../../assets/img/circle.png" alt="" />
              </div>
              <div class="ml-2">
                <span class="text-lg font-black">今日数据 </span>
                <span> 数据说话，言之凿凿</span>
              </div>
            </div>
            <div class="mt-4">
              <a href="javascript:;" class="text-red-400" @click="putAway">{{
                !showNowdata ? '展开' : '收起'
              }}</a>
            </div>
          </div>
          <!-- 每个时间内容 -->
          <div class="flex mt-1" v-if="showNowdata">
            <!-- 左侧时间 -->
            <div class="flex-1">
              <div class="flex">
                <div>上午时间</div>
                <div class="ml-16">工作记录及事项</div>
              </div>
              <div
                class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
              >
                <div class="w-1/4 bg-gray-100 flex items-center p-1">
                  <span> 08:00~09:00</span>
                </div>
                <div class="w-3/4 flex justify-between items-center">
                  <span></span>
                  <span class="mr-1" @click="openchildDialog(1)">
                    <img src="../../../assets/img/add.png" alt="" class="w-4"
                  /></span>
                </div>
              </div>
              <div
                class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
              >
                <div class="w-1/4 bg-gray-100 flex items-center p-1">
                  <span> 09:00~10:00</span>
                </div>
                <div class="w-3/4 flex justify-between items-center">
                  <span></span>
                  <span class="mr-1" @click="openchildDialog(2)">
                    <img src="../../../assets/img/add.png" alt="" class="w-4"
                  /></span>
                </div>
              </div>
              <div
                class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
              >
                <div class="w-1/4 bg-gray-100 flex items-center p-1">
                  <span> 10:00~11:00</span>
                </div>
                <div class="w-3/4 flex justify-between items-center">
                  <span></span>
                  <span class="mr-1" @click="openchildDialog(3)">
                    <img src="../../../assets/img/add.png" alt="" class="w-4"
                  /></span>
                </div>
              </div>
              <div
                class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
              >
                <div class="w-1/4 bg-gray-100 flex items-center p-1">
                  <span> 11:00~12:00</span>
                </div>
                <div class="w-3/4 flex justify-between items-center">
                  <span></span>
                  <span class="mr-1" @click="openchildDialog(4)">
                    <img src="../../../assets/img/add.png" alt="" class="w-4"
                  /></span>
                </div>
              </div>
            </div>
            <!-- 右侧时间 -->
            <div class="flex-1 ml-2">
              <div class="flex">
                <div>上午时间</div>
                <div class="ml-16">工作记录及事项</div>
              </div>
              <div
                class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
              >
                <div class="w-1/4 bg-gray-100 flex items-center p-1">
                  <span> 13:00~14:00</span>
                </div>
                <div class="w-3/4 flex justify-between items-center">
                  <span></span>
                  <span class="mr-1" @click="openchildDialog(5)">
                    <img src="../../../assets/img/add.png" alt="" class="w-4"
                  /></span>
                </div>
              </div>
              <div
                class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
              >
                <div class="w-1/4 bg-gray-100 flex items-center p-1">
                  <span> 14:00~15:00</span>
                </div>
                <div class="w-3/4 flex justify-between items-center">
                  <span></span>
                  <span class="mr-1" @click="openchildDialog(6)">
                    <img src="../../../assets/img/add.png" alt="" class="w-4"
                  /></span>
                </div>
              </div>
              <div
                class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
              >
                <div class="w-1/4 bg-gray-100 flex items-center p-1">
                  <span> 15:00~16:00</span>
                </div>
                <div class="w-3/4 flex justify-between items-center">
                  <span></span>
                  <span class="mr-1" @click="openchildDialog(7)">
                    <img src="../../../assets/img/add.png" alt="" class="w-4"
                  /></span>
                </div>
              </div>
              <div
                class="flex border-solid border-2 border-gray-100 rounded-md h-10 mb-1"
              >
                <div class="w-1/4 bg-gray-100 flex items-center p-1">
                  <span> 16:00~17:00</span>
                </div>
                <div class="w-3/4 flex justify-between items-center">
                  <span></span>
                  <span class="mr-1" @click="openchildDialog(8)">
                    <img src="../../../assets/img/add.png" alt="" class="w-4"
                  /></span>
                </div>
              </div>
            </div>
          </div>
          <!-- 子组件Dialog -->
          <childrenDialogVue
            :childata="showChilDialog"
            @Success="Success($event)"
            @closed="closed"
          />
        </div>
        <el-form
          ref="ruleFormRef"
          :model="formdata"
          :rules="rules"
          :size="formSize"
          status-icon
        >
          <!-- 今日总结 -->
          <div class="NoInput">
            <div class="flex justify-between items-center w-full">
              <!-- 今日总结表头 -->
              <div class="flex mt-4 items-center">
                <div class="flex">
                  <div class="w-6 h-6 mt-2">
                    <img src="../../../assets/img/circle.png" alt="" />
                  </div>
                  <div class="ml-2">
                    <span class="text-lg font-black">今日总结 </span>
                    <span> 日事日毕，日清日高</span>
                  </div>
                </div>
              </div>
              <!-- 评价 -->
              <div class="flex">
                <div class="flex">
                  <span>工作饱和:</span>
                  <span
                    v-if="formdata.radio1 === '差'"
                    class="w-6 h-6 bg-red-500 text-white rounded-md text-center"
                    >差</span
                  >
                  <span
                    v-else-if="formdata.radio1 === '中'"
                    class="w-6 h-6 bg-orange-300 text-white rounded-md text-center"
                    >中</span
                  >
                  <span
                    v-else-if="formdata.radio1 === '好'"
                    class="w-6 h-6 bg-green-500 text-white rounded-md text-center"
                    >好</span
                  >
                </div>
                <div class="flex">
                  <span>工作效率:</span>
                  <span
                    v-if="formdata.radio1 === '差'"
                    class="w-6 h-6 bg-red-500 text-white rounded-md text-center"
                    >差</span
                  >
                  <span
                    v-if="formdata.radio1 === '中'"
                    class="w-6 h-6 bg-orange-300 text-white rounded-md text-center"
                    >中</span
                  >
                  <span
                    v-if="formdata.radio1 === '好'"
                    class="w-6 h-6 bg-green-500 text-white rounded-md text-center"
                    >好</span
                  >
                </div>
                <div class="flex">
                  <span>工作质量:</span>
                  <span
                    v-if="formdata.radio2 === '差'"
                    class="w-6 h-6 bg-red-500 text-white rounded-md text-center"
                    >差</span
                  >
                  <span
                    v-else-if="formdata.radio2 === '中'"
                    class="w-6 h-6 bg-orange-300 text-white rounded-md text-center"
                    >中</span
                  >
                  <span
                    v-else-if="formdata.radio2 === '好'"
                    class="w-6 h-6 bg-green-500 text-white rounded-md text-center"
                    >好</span
                  >
                </div>
              </div>
              <!--  -->
            </div>
            <!-- 今日总结内容 -->
            <div class="border-solid border-2 border-gray-100">
              <!-- 时间利用以及内容阐述 -->
              <div class="h-8 leading-8 pl-2 bg-gray-200">
                <span class="text font-extrabold">时间利用及内容阐述</span>
              </div>
              <div class="p-2">
                <div>1、8个时间段考核中7个没工作内容，工作饱和度为好</div>
                <div>
                  <el-form-item prop="contant">
                    <el-input
                      v-model="formdata.contant"
                      placeholder="请按序号进行时间利用内容出参数，重复率不超过20%"
                    ></el-input
                  ></el-form-item>
                </div>
                <div class="flex justify-end items-center">
                  <span>工作效率：</span>
                  <el-radio-group
                    v-model="formdata.radio1"
                    class="ml-4"
                    @change="SummarizeRadio"
                  >
                    <el-radio label="好" size="large">好</el-radio>
                    <el-radio label="中" size="large">中</el-radio>
                    <el-radio label="差" size="large">差</el-radio>
                  </el-radio-group>
                </div>
              </div>
              <!-- 成果转换 -->
              <div
                class="h-8 leading-8 pl-2 bg-gray-200 flex items-center justify-between"
              >
                <div>
                  <span class="text font-extrabold">成果转换</span>
                  <span class="ml-8 text-xs">请点击右侧按钮添加成果转换</span>
                </div>
                <div
                  class="w-4 h-4 mr-3 cursor-pointer"
                  @click="openchildDialog(11)"
                >
                  <img src="../../../assets/img/add.png" alt="" />
                </div>
              </div>
              <div class="p-2">
                <div>
                  <span>{{ formdata.contant1 }}</span>
                  <span class="text-red-400">{{ formdata.radio3 }}</span>
                </div>
                <br />
                <div class="flex justify-end items-center">
                  <span>工作质量：</span>
                  <el-radio-group
                    v-model="formdata.radio2"
                    class="ml-4"
                    @change="SummarizeRadio1"
                  >
                    <el-radio label="好" size="large">好</el-radio>
                    <el-radio label="中" size="large">中</el-radio>
                    <el-radio label="差" size="large">差</el-radio>
                  </el-radio-group>
                </div>
              </div>
            </div>
          </div>
          <!-- 今日精进 -->
          <div class="NoInput">
            <div class="flex mt-4 items-center">
              <div class="flex">
                <div class="w-6 h-6 mt-2">
                  <img src="../../../assets/img/circle.png" alt="" />
                </div>
                <div class="ml-2">
                  <span class="text-lg font-black">今日精进 </span>
                  <span>理由千万，贵在自省</span>
                </div>
              </div>
            </div>
            <div class="border-solid border-2 border-gray-100">
              <div class="h-8 leading-8 pl-2 bg-gray-200 flex items-center">
                <span class="text font-extrabold">改进措施</span>
              </div>
              <div class="h-16">
                <el-form-item prop="Improve">
                  <el-input
                    placeholder="请按序列号排列进行时间利用内容出参数，重复率不超过20%"
                    v-model="formdata.Improve"
                  ></el-input>
                </el-form-item>
              </div>
              <div class="h-8 leading-8 pl-2 bg-gray-200 flex items-center">
                <span class="text font-extrabold">明日计划</span>
              </div>
              <div class="h-16">
                <el-form-item prop="plan">
                  <el-input
                    placeholder="请按序列号排列进行时间利用内容出参数，重复率不超过20%"
                    v-model="formdata.plan"
                  ></el-input>
                </el-form-item>
              </div>
            </div>
          </div>
        </el-form>
      </div>

      <template #footer>
        <span class="dialog-footer">
          <el-button @click="closes">关闭</el-button>
          <el-button type="primary" @click="dialogVisible = false"
            >提交</el-button
          >
        </span>
      </template>
    </el-dialog>
  </div>
</template>
<script lang="ts">
import { defineComponent, SetupContext, ref, reactive } from 'vue'
import childrenDialogVue from './childrenDialog.vue'
import type { FormInstance, FormRules } from 'element-plus'
// 控制子组件的弹窗
const childrenDialog = () => {
  // 打开子组件的dialog
  const openchildDialog = (val: any) => {
    showChilDialog.isOpen = true
    showChilDialog.showTime = val
  }
  // 子组件是否打开,子组件传值
  const showChilDialog = reactive({
    isOpen: false,
    showTime: 1
  })
  // 接受子组件发送的事件
  const closed = () => {
    showChilDialog.isOpen = false
  }
  return {
    openchildDialog,
    showChilDialog,
    closed
  }
}
export default defineComponent({
  name: '',
  components: {
    childrenDialogVue
  },
  props: {
    data: {
      type: Object
    }
  },
  emits: ['close'],
  setup(prop, SetupContext) {
    // const fdf = ref()
    // fdf.value = [
    //   { name: '好', v: 1 },
    //   { name: '中', v: 2 },
    //   { name: '差', v: 3 }
    // ]
    // const SummarizeRadio1dsd = (val: any) => {
    //   let obj = fdf.value.find((x: any) => (x.v = val))
    //   if (obj) {
    //     return obj.name
    //   } else {
    //     return '-'
    //   }
    // }

    // 表单数据
    const formdatademo = {
      // 今日数据的时间段
      start: 0,
      end: 0,
      // 成果转换内容
      contant1: [],
      // 成果转化单选框内容
      radio3: [],
      // 时间利用及内容阐述的内容
      contant: '',
      // 时间利用及内容和参数的单选框
      radio1: '差',
      radio2: '好',
      // 改进措施内容,
      Improve: '',
      // 明日计划内容
      plan: ''
    }
    const formdata = ref()
    formdata.value = JSON.parse(JSON.stringify(formdatademo))
    // 子组件点击成功传来的数据
    const Success = (data: any) => {
      formdata.value.contant1.push(data.contant1)
      formdata.value.radio3.push(data.radio1)
      // console.log(data)
    }
    // 表单的ref
    const ruleFormRef = ref<FormInstance>()
    // 表单校验规则
    const rules = reactive<FormRules>({
      contant: [
        {
          required: true,
          message: '请填写时间利用及内容阐述',
          trigger: 'blur'
        }
      ],
      Improve: [
        {
          required: true,
          message: '请填写改进措施',
          trigger: 'blur'
        }
      ],
      plan: [
        {
          required: true,
          message: '请填写明日计划',
          trigger: 'blur'
        }
      ]
    })
    //   点击收起今日数据
    const showNowdata = ref(false)
    const putAway = () => {
      showNowdata.value = !showNowdata.value
    }
    // 发送关闭事件给父组件
    const closes = () => {
      SetupContext.emit('close')
    }
    // 关闭dialog
    const closedOne = (val: any) => {
      showNowdata.value = false
      val.resetFields()
      formdata.value = JSON.parse(JSON.stringify(formdatademo))
    }
    return {
      ...childrenDialog(),
      Success,
      ruleFormRef,
      rules,
      formdata,
      closedOne,
      closes,
      putAway,
      showNowdata
    }
  }
})
</script>
<style lang="postcss" scoped>
.dialogClass {
  .NoInput {
    :deep(.el-input__inner) {
      border-top-width: 0px;
      border-left-width: 0px;
      border-right-width: 0px;
      border-bottom-width: 0px;
    }
  }
  :deep(.el-dialog__body) {
    padding: 0;
  }
}
</style>
