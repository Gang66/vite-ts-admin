<template>
  <div class="assetsa-AssetProcurement-index flex">
    <div class="mt-5 w-3/4">
      <!-- 数据筛选 -->
      <div>
        <el-card>
          <div class="flex justify-between items-center">
            <div class="font-black">数据筛选</div>
            <div class="flex items-center">
              <div class="flex mr-4">
                <span
                  @click="changetime(0)"
                  class="mr-4 text-gray-400 cursor-pointer"
                  :class="{ 'text-blue-400': variables.currentday === 0 }"
                  >最近7天</span
                >
                <span
                  class="mr-4 text-gray-400 cursor-pointer"
                  :class="{ 'text-blue-400': variables.currentday === 1 }"
                  @click="changetime(1)"
                  >日</span
                >
                <span
                  :class="{ 'text-blue-400': variables.currentday === 2 }"
                  class="mr-4 text-gray-400 cursor-pointer"
                  @click="changetime(2)"
                  >周</span
                >
                <span
                  :class="{ 'text-blue-400': variables.currentday === 3 }"
                  class="mr-4 text-gray-400 cursor-pointer"
                  @click="changetime(3)"
                  >月</span
                >
                <span
                  :class="{ 'text-blue-400': variables.currentday === 4 }"
                  class="mr-4 text-gray-400 cursor-pointer"
                  @click="changetime(4)"
                  >季</span
                >
                <span
                  :class="{ 'text-blue-400': variables.currentday === 5 }"
                  class="text-gray-400 cursor-pointer"
                  @click="changetime(5)"
                  >年</span
                >
              </div>
              <div class="flex items-center">
                <el-date-picker
                  class="mr-2"
                  v-model="query.value1"
                  type="daterange"
                  range-separator="-"
                  start-placeholder="开始时间"
                  end-placeholder="结束时间"
                />
                <el-select placeholder="请选择" v-model="query.department">
                  <el-option
                    v-for="item in options"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value"
                  />
                </el-select>
              </div>
            </div>
          </div>
        </el-card>
      </div>
      <!-- ECharts图表 -->
      <div class="flex justify-between m-2 w-9/10">
        <!-- 左侧部门采购费用 -->

        <div id="myChart" class="h-96 w-2/5 bg-white p-2"></div>

        <!-- 右侧采购费用对比 -->
        <div id="myChart1" class="h-96 w-3/5 bg-white p-2 ml-2"></div>
      </div>
      <!-- 下列table表格 -->
      <div>
        <el-card> <purchaseTable /></el-card>
      </div>
    </div>
    <div class="mt-5 ml-3 w-1/5 rounded-md">
      <rightDialogVue />
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, onMounted, reactive, ref } from 'vue'
import rightDialogVue from '../../Components/rightDialog.vue'
import purchaseTable from './components/purchaseTable.vue'

import * as echarts from 'echarts'

export default defineComponent({
  name: '',
  components: {
    rightDialogVue,
    purchaseTable
  },
  setup() {
    // 定义的所有变量
    const variables = reactive({
      // 顶部筛选的高亮
      currentday: 0
    })

    /**
     * 顶部筛选代码
     */
    // 筛选的数据
    const query = reactive({
      // 筛选时间的开始和结束
      value1: [],
      // 筛选的部门
      department: ''
    })
    // 切换时间时的高亮以及数据更新
    const changetime = (val: any) => {
      if (val === 0) {
        datademo.value = datademo1
        dataright.value = dataright1
        chart()
        chart1()
      } else if (val === 1) {
        datademo.value = datademo2
        dataright.value = dataright3
        chart()
        chart1()
      }
      variables.currentday = val
    }
    // 筛选的部门数据
    const options = [
      {
        value: 'Option1',
        label: '测试1'
      },
      {
        value: 'Option2',
        label: '测试2'
      },
      {
        value: 'Option3',
        label: '测试3'
      },
      {
        value: 'Option4',
        label: '测试4'
      },
      {
        value: 'Option5',
        label: '测试5'
      }
    ]
    /**
     * 顶部筛选代码结束
     */

    /**
     * 左侧ECharts
     */
    let datademo = ref({
      money: [430, 330, 480, 220],
      Xtitle: ['直属部门', '第一大区', '第二大区', '销售大区'],
      totalMoney: '8600'
    })
    const datademo1 = {
      money: [430, 330, 480, 220],
      Xtitle: ['直属部门', '第一大区', '第二大区', '销售大区'],
      totalMoney: '8600'
    }
    const datademo2 = {
      money: [30, 330, 80, 220],
      Xtitle: ['直属部门', '第一大区', '第二大区', '销售大区'],
      totalMoney: '8600'
    }
    const datademo3 = {
      money: [230, 330, 480, 20],
      Xtitle: ['直属部门', '第一大区', '第二大区', '销售大区'],
      totalMoney: '8600'
    }
    const chart = () => {
      let myChart = echarts.init(document.getElementById('myChart')!)
      myChart.setOption({
        title: [
          {
            text: '部门采购费用',

            textStyle: {
              fontSize: 16
            }
          },
          {
            text: '记录审批通过的采购单',
            left: 110,
            top: 3,
            textStyle: {
              fontSize: 12,
              color: 'rgba(172, 172, 172)'
            }
          },
          {
            text: `${datademo.value.totalMoney}元`,
            left: '80%',
            textStyle: {
              fontSize: 16
            }
          }
        ],
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        xAxis: {
          type: 'category',
          data: datademo.value.Xtitle
        },
        yAxis: [
          {
            type: 'value',
            splitLine: {
              show: true,
              lineStyle: {
                type: 'dashed'
              }
            }
          }
        ],
        series: [
          {
            name: '费用',
            data: datademo.value.money,
            type: 'bar',
            showBackground: true,
            barWidth: 30,
            backgroundStyle: {
              color: 'rgba(0,0,0,0)'
            },
            itemStyle: {
              normal: {
                color: '#0091ff'
              }
            }
          }
        ]
      })
      window.onresize = function () {
        myChart.resize()
      }
    }
    /**
     * 左侧ECharts结束
     */

    /**
     * 右侧ECharts
     */
    let dataright = ref({
      money: [100, 200, 100, 300, 200, 400, 100, 500, 300, 200, 400, 300],
      Xtitle: [
        '1月',
        '2月',
        '3月',
        '4月',
        '5月',
        '6月',
        '7月',
        '8月',
        '9月',
        '10月',
        '11月',
        '12月'
      ]
    })
    const dataright1 = {
      money: [100, 200, 100, 300, 200, 400, 100, 500, 300, 200, 400, 300],
      Xtitle: [
        '1月',
        '2月',
        '3月',
        '4月',
        '5月',
        '6月',
        '7月',
        '8月',
        '9月',
        '10月',
        '11月',
        '12月'
      ]
    }
    const dataright2 = {
      money: [100, 500, 100, 300, 200, 400, 100, 500, 300, 200, 400, 300],
      Xtitle: [
        '1月',
        '2月',
        '3月',
        '4月',
        '5月',
        '6月',
        '7月',
        '8月',
        '9月',
        '10月',
        '11月',
        '12月'
      ]
    }
    const dataright3 = {
      money: [200, 300, 100, 300, 200, 400, 100, 500, 300, 200, 400, 100],
      Xtitle: [
        '1月',
        '2月',
        '3月',
        '4月',
        '5月',
        '6月',
        '7月',
        '8月',
        '9月',
        '10月',
        '11月',
        '12月'
      ]
    }
    const chart1 = () => {
      let myChart1 = echarts.init(document.getElementById('myChart1')!)
      myChart1.setOption({
        title: [
          {
            text: '部门费用对比',

            textStyle: {
              fontSize: 16
            }
          }
        ],
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: dataright.value.Xtitle
        },
        yAxis: {
          type: 'value',
          splitLine: {
            show: true,
            lineStyle: {
              type: 'dashed'
            }
          }
        },
        series: [
          {
            name: '费用',
            data: dataright.value.money,
            type: 'line'
          }
        ]
      })
      window.onresize = function () {
        myChart1.resize()
      }
    }
    /**
     * 右侧ECharts结束
     */

    onMounted(() => {
      chart()
      chart1()
    })
    return {
      variables,
      query,
      changetime,
      options,
      datademo,
      dataright
    }
  }
})
</script>
<style lang="postcss" scoped>
.assetsa-AssetProcurement-index {
  :deep(.el-date-editor) {
    width: 220px;
  }
}
</style>
