<template>
  <div>
    <div>
      <!-- 创新直通车 -->
      <div class="rounded-md bg-white h-40">
        <div class="w-full h-10 bg-blue-400 rounded-md leading-10 pl-3">
          <span class="text-white">创新直通车</span>
        </div>
        <div class="rightbut flex flex-col mt-3">
          <div class="w-full ml-6">
            <el-button
              @click="rightbtn('1')"
              style="width: 40%; height: 40px"
              round
              color="#00abff"
              >培训调研</el-button
            >
            <el-button
              @click="rightbtn('2')"
              style="width: 40%; height: 40px"
              round
              color="#f6bc00"
              >意见建议</el-button
            >
          </div>
          <div class="mt-3 w-full ml-6">
            <el-button
              @click="rightbtn('3')"
              style="width: 40%; height: 40px"
              round
              color="#57d7fd"
              >创新举措</el-button
            >
            <el-button
              @click="rightbtn('4')"
              style="width: 40%; height: 40px"
              round
              color="#1fedcb"
              >其他建议</el-button
            >
          </div>
        </div>
      </div>
      <!-- 常用工具 -->
      <div class="rounded-md bg-white mt-3">
        <div class="w-full h-10 bg-blue-400 rounded-md leading-10 pl-3">
          <span class="text-white">常用工具</span>
        </div>
        <div class="flex flex-wrap p-2">
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
          <div class="flex flex-col w-1/5 ml-1">
            <div class="w-14 h-14 bg-blue-200 rounded-md"></div>
            <span class="text-xs">发起公告</span>
          </div>
        </div>
      </div>
      <!-- 排行榜 -->
      <div class="rounded-md bg-white mt-3">
        <div class="w-full h-10 bg-blue-400 rounded-md leading-10 pl-3">
          <span class="text-white">排行榜</span>
        </div>
        <div class="pl-4 pb-3">
          <el-tabs v-model="activeName" class="demo-tabs">
            <el-row class="text-center mb-2">
              <el-col :span="5"><span class="font-black">排名</span></el-col>
              <el-col :span="8"><span class="font-black">事业部</span></el-col>
              <el-col :span="8"
                ><span class="font-black">培训专员</span></el-col
              >
            </el-row>
            <el-tab-pane label="邀约排行" name="first">
              <div>
                <el-row class="text-center">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      1
                    </div></el-col
                  >
                  <el-col :span="8"><span>集团总部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      2
                    </div></el-col
                  >
                  <el-col :span="8"><span>潍坊事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      3
                    </div></el-col
                  >
                  <el-col :span="8"><span>济南事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      4
                    </div></el-col
                  >
                  <el-col :span="8"><span>润扬事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      5
                    </div></el-col
                  >
                  <el-col :span="8"><span>南京事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      6
                    </div></el-col
                  >
                  <el-col :span="8"><span>银川事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      7
                    </div></el-col
                  >
                  <el-col :span="8"><span>邯郸事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      8
                    </div></el-col
                  >
                  <el-col :span="8"><span>湖高事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      9
                    </div></el-col
                  >
                  <el-col :span="8"><span>北京事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      10
                    </div></el-col
                  >
                  <el-col :span="8"><span>寒亭事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
              </div>
            </el-tab-pane>
            <el-tab-pane label="面试排行" name="second">
              <div>
                <el-row class="text-center">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      1
                    </div></el-col
                  >
                  <el-col :span="8"><span>寒亭总部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      2
                    </div></el-col
                  >
                  <el-col :span="8"><span>潍坊事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      3
                    </div></el-col
                  >
                  <el-col :span="8"><span>济南事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      4
                    </div></el-col
                  >
                  <el-col :span="8"><span>润扬事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      5
                    </div></el-col
                  >
                  <el-col :span="8"><span>南京事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      6
                    </div></el-col
                  >
                  <el-col :span="8"><span>银川事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      7
                    </div></el-col
                  >
                  <el-col :span="8"><span>邯郸事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      8
                    </div></el-col
                  >
                  <el-col :span="8"><span>湖高事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      9
                    </div></el-col
                  >
                  <el-col :span="8"><span>北京事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
                <el-row class="text-center mt-2">
                  <el-col :span="5"
                    ><div class="w-7 h-7 bg-blue-100 ml-4 rounded-md">
                      10
                    </div></el-col
                  >
                  <el-col :span="8"><span>集团事业部</span></el-col>
                  <el-col :span="8"><span>无</span></el-col>
                </el-row>
              </div>
            </el-tab-pane>
          </el-tabs>
        </div>
      </div>
      <!-- 个人素养展示区 -->
      <div
        class="rounded-md mt-3 bg-gradient-to-b from-green-400 to-blue-500 h-40 p-3"
      >
        <h2 class="text-white">个人素养展示区</h2>
        <div class="flex justify-around mt-6">
          <div class="flex flex-col items-center">
            <span
              class="h-12 w-12 text-gray-400 rounded-md bg-yellow-200 text-center"
            >
              头像
            </span>
            <span class="text-white mt-2">第一名：张铁锤</span>
          </div>
          <div class="flex flex-col items-center">
            <span
              class="h-12 w-12 text-gray-400 rounded-md bg-yellow-200 text-center"
            >
              小心心
            </span>
            <span class="text-white mt-2">获赞:10个</span>
          </div>
        </div>
      </div>
    </div>
    <innovationDialog :data="innovationData" @closed="closed" />
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import innovationDialog from '/@/views/Project/components/innovationDialog.vue'
export default defineComponent({
  name: '',
  components: {
    innovationDialog
  },
  setup() {
    const activeName = ref('first')
    // 监听关闭按钮
    const closed = () => {
      innovationData.dialogVisible = false
    }
    const rightbtn = (val: any) => {
      innovationData.userInfo.number = val
      innovationData.dialogVisible = true
    }
    const innovationData = reactive({
      dialogVisible: false,
      userInfo: {
        number: '1'
      }
    })
    return { innovationData, rightbtn, closed, activeName }
  }
})
</script>
<style scoped></style>
