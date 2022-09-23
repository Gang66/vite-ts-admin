<template>
  <div class="Dashboard-workplace-index">
    <div class="m-8">
      <el-button @click="openHrDialog" type="success" class="m-2"
        >HR测评表</el-button
      >
    </div>
    <HRdialog :data="hrDialogData" @close="closeHrDialog($event)" />
    <hr />

    <Earch />
  </div>
</template>
<script lang="ts">
//HR测评表
const hrDialog = () => {
  const hrDialogData = ref({
    isDialog: false,
    title: 'HR测评表',
    arr: [],
    obj: {
      name: '张铁锤',
      gangwei: '技术员',
      shiyebu: '潍坊事业部',
      bumen: '技术部',
      mianshiguan: '麦克狐',
      riqi: '2022-02-01'
    },
    id: 0
  })
  // 打开HR测评表dialog
  const openHrDialog = () => {
    hrDialogData.value.isDialog = true
  }
  // 关闭HR测评表dialog
  const closeHrDialog = () => {
    hrDialogData.value.isDialog = false
  }

  return {
    hrDialogData,
    openHrDialog,
    closeHrDialog
  }
}

// 测试
const ceshiDialog = () => {
  const ceshiDialogData = ref({
    isDialog: false,
    title: '测试',
    arr: [],
    id: 0
  })
  // 打开测试dialog
  const openCeshiDialog = () => {
    ceshiDialogData.value.isDialog = true
  }
  // 关闭测试dialog
  const closeCeshiDialog = () => {
    ceshiDialogData.value.isDialog = false
  }

  return {
    ceshiDialogData,
    openCeshiDialog,
    closeCeshiDialog
  }
}

import { ref } from '@vue/reactivity'
import HRdialog from './_Components/HRdialog.vue'
import CeshiDialog from './_Components/ceshiDialog.vue'
import Earch from './_Components/Earch.vue'

name: 'Workplace'
export default {
  components: {
    HRdialog,
    CeshiDialog,
    Earch
  },
  setup() {
    const isShowDialog = ref(false)
    const form = ref({
      name: ''
    })
    return {
      form,
      isShowDialog,
      ...hrDialog(),
      ...ceshiDialog()
    }
  }
}
</script>
<style lang="postcss" scoped>
.inputs ::v-deep(.el-input__inner) {
  width: 200px;
}
.twoInput ::v-deep(.el-input__inner) {
  width: 400px;
}
</style>
