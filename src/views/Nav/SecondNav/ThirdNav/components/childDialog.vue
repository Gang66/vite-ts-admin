<template>
  <div class="Nav-SecondNav-ThirdNav-componends-childDialog">
    <el-dialog
      v-model="childata.showChildDialog"
      title="Tips"
      width="30%"
      :before-close="handleClose"
    >
      <!-- 头部 -->
      <div
        class="bg-blue-600 w-full h-10 flex justify-between items-center pl-2"
      >
        <h2 class="text-white">上传素材</h2>
        <div class="mr-1 flex items-center">
          <div
            class="h-5 w-5 bg-slate-300 ml-2 rounded-full flex items-center justify-center"
            @click="handleClose(ruleFormRef)"
          >
            <span class="text-lg text-white cursor-pointer">×</span>
          </div>
        </div>
      </div>
      <div>
        <el-upload
          class="avatar-uploader"
          action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15"
          :show-file-list="false"
          :on-success="handleAvatarSuccess"
          :before-upload="beforeAvatarUpload"
        >
          <img v-if="imageUrl" :src="imageUrl" class="avatar" />

          <!-- <el-icon v-else class="avatar-uploader-icon"><Plus /></el-icon> -->
          <div v-else class="bg-gray-400 h-36 w-36">添加</div>
        </el-upload>
      </div>
      <div class="flex flex-col ml-2">
        <span class="text-red-400">说明：</span>
        <span> 1：可以同时选择多张图片，点击“上传至服务器”批量上传；</span>
        <span> 2：所有文件全部上传后可根据左右箭头调整文件位置；</span>
        <span> 3：点击“确定”后上传的图片才生效</span>
      </div>
      <template #footer>
        <span class="dialog-footer">
          <el-button @click="handleClose">关闭</el-button>
          <el-button type="primary" @click="dialogVisible = false"
            >确定</el-button
          >
        </span>
      </template>
    </el-dialog>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue'
import { ElMessageBox, ElMessage } from 'element-plus'
// import { Plus } from '@element-plus/icons-vue'
import type { UploadProps } from 'element-plus'

export default defineComponent({
  name: '',
  props: {
    childata: {
      type: Object
    }
  },
  emits: ['closeChildDialog'],
  setup(prop, tcx) {
    //   关闭dialog
    const handleClose = (done: () => void) => {
      ElMessageBox.confirm('确定要关闭弹窗嘛', {
        confirmButtonText: '确定',
        cancelButtonText: '取消'
      })
        .then(() => {
          tcx.emit('closeChildDialog')
          done()
        })
        .catch(() => {
          // catch error
        })
    }

    const imageUrl = ref('')
    const handleAvatarSuccess: UploadProps['onSuccess'] = (
      response,
      uploadFile
    ) => {
      imageUrl.value = URL.createObjectURL(uploadFile.raw!)
    }

    const beforeAvatarUpload: UploadProps['beforeUpload'] = (rawFile: any) => {
      //   if (rawFile.type !== 'image/png') {
      //     ElMessage.error('必须为图片的格式')
      //     return false
      //   } else if (rawFile.size / 1024 / 1024 > 2) {
      //     ElMessage.error('图片大小不能超过2MB')
      //     return false
      //   }
      return true
    }
    return { handleClose, handleAvatarSuccess, imageUrl, beforeAvatarUpload }
  }
})
</script>
<style lang="postcss" scoped>
.Nav-SecondNav-ThirdNav-componends-childDialog {
  :deep(.el-dialog__body) {
    padding: 0;
  }
  .avatar-uploader .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
  .avatar-uploader .el-upload {
    border: 1px dashed var(--el-border-color);
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition: var(--el-transition-duration-fast);
  }

  .avatar-uploader .el-upload:hover {
    border-color: var(--el-color-primary);
  }

  .el-icon.avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    text-align: center;
  }
}
</style>
