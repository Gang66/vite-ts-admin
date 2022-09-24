<template>
  <div class="Dashboard-Welcome-index flex">
    <div class="mt-3 ml-20 w-3/4">
      <el-card>
        <h2>产品库配置</h2>
        <el-tabs v-model="activeName" class="demo-tabs">
          <el-tab-pane label="产品分类" name="first">
            <div class="flex">
              <div class="w-1/5">
                <h2>分类树</h2>
                <el-tree
                  :data="data"
                  :props="defaultProps"
                  @node-click="handleNodeClick"
                />
              </div>
              <div class="rightTable w-3/4">
                <h2 class="mb-2">子类数据</h2>
                <el-table :data="tableData" style="width: 100%">
                  <el-table-column type="selection" width="55" />
                  <el-table-column label="编码" width="120" prop="coding" />

                  <el-table-column
                    label="名称"
                    prop="name"
                    show-overflow-tooltip
                  />
                  <el-table-column
                    label="所属上级"
                    prop="superior"
                    show-overflow-tooltip
                  />
                  <el-table-column
                    label="排序"
                    prop="sort"
                    show-overflow-tooltip
                  />
                  <el-table-column label="操作">
                    <template #default="{ row }">
                      <div class="flex">
                        <el-button type="warning">修改</el-button>
                        <el-button type="danger">删除</el-button>
                      </div>
                    </template>
                  </el-table-column>
                </el-table>
              </div>
            </div>
          </el-tab-pane>
          <el-tab-pane label="法兰配对" name="second">Config</el-tab-pane>
          <el-tab-pane label="电动配对" name="third">Role</el-tab-pane>
          <el-tab-pane label="气动配对" name="fourth">Task</el-tab-pane>
          <el-tab-pane label="垫片配对" name="five">Task</el-tab-pane>
          <el-tab-pane label="螺栓配对" name="six">Task</el-tab-pane>
        </el-tabs>
      </el-card>
    </div>
    <div class="mt-3 ml-10 w-1/5 rounded-md"><rightDialog /></div>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue'
import rightDialog from '/@/views/Components/rightDialog.vue'
const one = () => {
  /**
   * 第一个页面的树形空间相应内容
   */
  interface Tree {
    label: string
    children?: Tree[]
  }
  // 点击显示相应树形内容
  const handleNodeClick = (data: Tree) => {
    console.log(data)
  }
  const data: Tree[] = [
    {
      label: '法兰盘',
      children: [
        {
          label: '板式平焊法兰（PL）'
        },
        {
          label: '带颈平焊法兰（SO）'
        },
        {
          label: '带颈对焊法兰（WN）'
        },
        {
          label: '承插焊法兰（SW）'
        },
        {
          label: '螺纹法兰（Th）'
        },
        {
          label: '整体法兰'
        },
        {
          label: '盲板/法兰盖（BL）'
        },
        {
          label: '对焊环松套法兰（PJ/SE）'
        },
        {
          label: '平焊环松套法兰（PJ/RJ）'
        },
        {
          label: '中线对夹蝶法兰（DF/PL）'
        }
      ]
    },
    {
      label: '气动装置',
      children: [
        {
          label: 'AT双作用气缸'
        },
        {
          label: 'AW双作用气缸'
        },
        {
          label: 'JSC双作用直行程气缸'
        },
        {
          label: '其他系列气缸'
        },
        {
          label: 'ATE单作用气缸'
        },
        {
          label: 'AWS单作用气缸'
        },
        {
          label: 'JSCS单作用直行程气缸'
        }
      ]
    },
    {
      label: '电动装置',
      children: [
        {
          label: '直行程电动执行器'
        },
        {
          label: 'BZ系列-普通开关型'
        },
        {
          label: '扬修系列'
        },
        {
          label: '川仪系列'
        },
        {
          label: '罗托克系列'
        },
        {
          label: '伯纳德系列'
        },
        {
          label: 'Q系列-普通开关型'
        },
        {
          label: 'Qz系列-智能开关型'
        },
        {
          label: 'DZW系列-普通开关型'
        }
      ]
    },
    {
      label: '垫片',
      children: [
        {
          label: '石棉垫'
        },
        {
          label: '四氟垫'
        },
        {
          label: '橡胶垫'
        },
        {
          label: '金属石墨垫-内外环'
        },
        {
          label: '金属石墨垫-基础型'
        },
        {
          label: '金属石墨垫-内环'
        },
        {
          label: '金属石墨垫-外环'
        },
        {
          label: '金属缠绕垫'
        }
      ]
    },
    {
      label: '标准件',
      children: [
        {
          label: '8.8级双头螺栓'
        },
        {
          label: '8.8级对夹式螺栓'
        },
        {
          label: '4.8级双头螺栓'
        },
        {
          label: '4.8级对夹式螺栓'
        },
        {
          label: '不锈钢双头螺栓'
        },
        {
          label: '不锈钢对夹式螺栓'
        }
      ]
    },
    {
      label: '电动附件',
      children: [
        {
          label: '电动控制箱'
        }
      ]
    },
    {
      label: '气动附件',
      children: [
        {
          label: '成套气动附件'
        },
        {
          label: '板式电磁阀'
        },
        {
          label: '定位器'
        },
        {
          label: '减压过滤油雾器'
        },
        {
          label: '限位开关'
        },
        {
          label: '气动手轮装置'
        },
        {
          label: '气源三联件'
        }
      ]
    }
  ]
  const defaultProps = {
    children: 'children',
    label: 'label'
  }
  /**
   * 树形控件结束
   */
  /**
   * 右侧table栏数据
   */
  interface User {
    coding: string
    name: string
    superior: string
    sort: number
  }
  const tableData: User[] = [
    {
      coding: 'SMD',
      name: '石棉垫',
      superior: '垫片',
      sort: 0
    },
    {
      coding: 'SFD',
      name: '四氟垫',
      superior: '垫片',
      sort: 0
    },
    {
      coding: 'XJD',
      name: '橡胶垫',
      superior: '垫片',
      sort: 0
    },
    {
      coding: 'NWQJSSM',
      name: '金属石墨垫-内外环',
      superior: '垫片',
      sort: 0
    }
  ]
  return { handleNodeClick, data, defaultProps, tableData }
}
export default defineComponent({
  name: '',
  components: {
    rightDialog
  },
  setup() {
    /**
     * tabs栏切换
     */
    const activeName = ref('first')

    return { ...one(), activeName }
  }
})
</script>
<style>
.el-table__header {
  background-color: red;
}
</style>
