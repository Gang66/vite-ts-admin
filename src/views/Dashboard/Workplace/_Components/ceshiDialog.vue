<template>
  <el-dialog
    v-model="data.isDialog"
    :title="data.title"
    width="820px"
    custom-class="dsd"
  >
    3333
  </el-dialog>
</template>
<script lang="ts">
import { defineComponent, ref, SetupContext } from 'vue'
import type { FormInstance, FormRules } from 'element-plus'

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
        id: 0
      }
    }
  },
  emits: ['close'],
  setup(props, context: SetupContext) {
    const Close = () => {
      context.emit('close', '')
    }
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

    return {
      Close,
      Confirm
    }
  }
})
</script>
<style lang="postcss" scoped>
.dsd {
  :deep(.el-dialog__header) {
    background-color: #516bdb;
    color: white;
  }
  :deep(.el-dialog__title) {
    color: white;
  }
}
</style>
