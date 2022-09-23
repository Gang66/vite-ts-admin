<template>
  <div id="Dashboard-workplace-components-Earch">
    <div
      class="h-auto w-1/2 border-solid border-2 rounded-md p-1 border-blue-300"
    >
      <div class="flex items-center relative w-1/4" @mouseleave="NoShowChange">
        <span> {{ TitleContant }}</span>
        <span
          @mouseenter="showChange"
          style="
            width: 0;
            height: 0;
            border-right: 5px solid transparent;
            border-left: 5px solid transparent;
            border-top: 5px solid #333;
          "
        ></span>
      </div>
      <div
        @mouseenter="showChange"
        @mouseleave="NoShowChange"
        v-if="isShow"
        class="cursor-pointer flex flex-col border-solid border-2 rounded-md w-1/4 ml-2 p-1 moreTitle"
      >
        <span
          @click="changeTitle(item)"
          v-for="(item, index) in allLook"
          :key="index"
          >{{ item }}</span
        >
      </div>
      <div id="myChart" class="h-96 w-full"></div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, onMounted, reactive, ref } from 'vue'
import * as echarts from 'echarts'
export default defineComponent({
  name: '',
  setup() {
    // 是否显示切换面板
    const isShow = ref(false)
    // 鼠标移入事件显示
    const showChange = () => {
      isShow.value = true
    }
    // 鼠标移出事件隐藏
    const NoShowChange = () => {
      isShow.value = false
    }
    const TitleContant = ref('部门分布看板')
    // 点击切换头部标签
    const changeTitle = (val: any) => {
      TitleContant.value = val
      if (val === '部门分布看板') {
        datademo.value = datademo1
        chart()
      } else if (val === '事业部分布看板') {
        datademo.value = datademo2
        chart()
      } else if (val === '集团分布看板') {
        datademo.value = datademo3
        chart()
      }
    }
    // 图表模块数量
    const allLook = reactive(['部门分布看板', '事业部分布看板', '集团分布看板'])
    let datademo = ref({
      money: [220, 20, 160, 200],
      number: [11, 8, 5, 20],
      Xtitle: ['业务一部', '业务二部', '业务三部', '业务四部']
    })
    const datademo1 = {
      money: [220, 220, 160, 200],
      number: [11, 8, 5, 20],
      Xtitle: ['业务一部', '业务二部', '业务三部', '业务四部']
    }
    const datademo2 = {
      money: [50, 150, 200, 123, 221, 22],
      number: [2, 6, 8, 11, 3, 21],
      Xtitle: [
        '潍坊事业部',
        '润扬事业部',
        '济南事业部',
        '银川事业部',
        '寒亭事业部'
      ]
    }
    const datademo3 = {
      money: [250, 1, 100],
      number: [20, 10, 5],
      Xtitle: ['部门分布看板', '事业部分布看板', '集团分布看板']
    }
    onMounted(() => {
      chart()
    })
    const chart = () => {
      let myChart = echarts.init(document.getElementById('myChart')!)
      myChart.setOption({
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
            crossStyle: {
              color: '#999'
            }
          }
        },
        toolbox: {
          feature: {
            dataView: { show: true, readOnly: false },
            magicType: { show: true, type: ['line', 'bar'] },
            restore: { show: true },
            saveAsImage: { show: true }
          }
        },
        legend: {
          data: ['金额', '数量']
        },
        xAxis: [
          {
            type: 'category',
            data: datademo.value.Xtitle,
            axisPointer: {
              type: 'shadow'
            }
          }
        ],
        yAxis: [
          {
            type: 'value',
            name: '金额',
            min: 0,
            max: 250,
            interval: 50,
            axisLabel: {
              // formatter: '{value} '
            }
          },
          {
            type: 'value',
            name: '数量',
            min: 0,
            max: 25,
            interval: 5
          }
        ],
        series: [
          {
            name: '金额',
            type: 'bar',
            data: datademo.value.money
          },
          {
            name: '数量',
            type: 'bar',
            yAxisIndex: 1,
            data: datademo.value.number
          }
        ]
      })
      window.onresize = function () {
        myChart.resize()
      }
    }

    return {
      datademo,
      allLook,
      showChange,
      isShow,
      NoShowChange,
      changeTitle,
      TitleContant
    }
  }
})
</script>
<style scoped></style>
