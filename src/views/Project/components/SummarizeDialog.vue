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
          <childrenDialogVue :childata="showChilDialog" @closed="closed" />
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
                    v-if="Evaluation === '差'"
                    class="w-6 h-6 bg-red-500 text-white rounded-md text-center"
                    >差</span
                  >
                  <span
                    v-if="Evaluation === '中'"
                    class="w-6 h-6 bg-orange-300 text-white rounded-md text-center"
                    >中</span
                  >
                  <span
                    v-if="Evaluation === '好'"
                    class="w-6 h-6 bg-green-500 text-white rounded-md text-center"
                    >好</span
                  >
                </div>
                <div class="flex">
                  <span>工作效率:</span>
                  <span
                    v-if="Evaluation2 === '差'"
                    class="w-6 h-6 bg-red-500 text-white rounded-md text-center"
                    >差</span
                  >
                  <span
                    v-if="Evaluation2 === '中'"
                    class="w-6 h-6 bg-orange-300 text-white rounded-md text-center"
                    >中</span
                  >
                  <span
                    v-if="Evaluation2 === '好'"
                    class="w-6 h-6 bg-green-500 text-white rounded-md text-center"
                    >好</span
                  >
                </div>
                <div class="flex">
                  <span>工作质量:</span>
                  <span
                    v-if="Evaluation3 === '差'"
                    class="w-6 h-6 bg-red-500 text-white rounded-md text-center"
                    >差</span
                  >
                  <span
                    v-if="Evaluation3 === '中'"
                    class="w-6 h-6 bg-orange-300 text-white rounded-md text-center"
                    >中</span
                  >
                  <span
                    v-if="Evaluation3 === '好'"
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
                <div></div>
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
                  <el-input v-model="formdata.Improve"></el-input>
                </el-form-item>
              </div>
              <div class="h-8 leading-8 pl-2 bg-gray-200 flex items-center">
                <span class="text font-extrabold">明日计划</span>
              </div>
              <div class="h-16">
                <el-form-item prop="plan">
                  <el-input v-model="formdata.plan"></el-input>
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
    // 点击时间利用以及内容阐述的change事件
    const SummarizeRadio = (val: any) => {
      if (val === '好') {
        Evaluation2.value = '好'
      } else if (val === '中') {
        Evaluation2.value = '中'
      } else if (val === '差') {
        Evaluation2.value = '差'
      }
    }
    const SummarizeRadio1 = (val: any) => {
      if (val === '好') {
        Evaluation3.value = '好'
      } else if (val === '中') {
        Evaluation3.value = '中'
      } else if (val === '差') {
        Evaluation3.value = '差'
      }
    }
    const formdata = reactive({
      // 时间利用及内容阐述的内容
      contant: '',
      // 时间利用及内容和参数的单选框
      radio1: '',
      radio2: '',
      // 改进措施内容,
      Improve: '',
      // 明日计划内容
      plan: ''
    })
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
    // 工作评价 差？ 好？ 中？
    const Evaluation = ref('差')
    const Evaluation2 = ref('中')
    const Evaluation3 = ref('好')
    //   点击收起今日数据
    const showNowdata = ref(false)
    const putAway = () => {
      showNowdata.value = !showNowdata.value
    }
    // 发送关闭事件给父组件
    const closes = () => {
      SetupContext.emit('close')
    }
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
    // 关闭dialog
    const closedOne = (val: any) => {
      showNowdata.value = false
      val.resetFields()
    }
    return {
      ruleFormRef,
      rules,
      formdata,
      SummarizeRadio1,
      SummarizeRadio,
      Evaluation3,
      Evaluation2,
      Evaluation,
      closedOne,
      closes,
      putAway,
      showNowdata,
      showChilDialog,
      openchildDialog,
      closed
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
