<template>
  <div>资产记录</div>
  <el-table border :data="testDatas" style="width: 100%'">
    <el-table-column type="selection" width="50"></el-table-column>
    <el-table-column
      v-for="item in columnList"
      :key="item.prop"
      :label="item.label"
      :prop="item.prop"
    >
      <template #default="scope">
        {{ scope.row[item.prop] }}
        <!-- <p
          v-show="scope.row[item.prop].show"
          @dblclick="scope.row[item.prop].row = false"
        >
          {{ item.label }}
        </p>
        <el-input
          v-show="!scope.row[item.prop].show"
          v-model="scope.row[item.prop].content"
          @blur="scope.row[column.prop].show = true"
        ></el-input> -->
      </template>
    </el-table-column>
  </el-table>
</template>
<script lang="ts">
import { defineComponent, reactive } from 'vue'
export default defineComponent({
  name: '',
  setup() {
    const columnList = reactive([
      { prop: 'name', label: '姓名', show: true },
      { prop: 'age', label: '年龄', show: true },
      { prop: 'city', label: '城市', show: true },
      { prop: 'tel', label: '电话', show: true }
    ])
    const testDatas = reactive([
      {
        No: 1,
        name: '张三',
        age: 24,
        city: '广州',
        tel: '1231561323',
        show: true
      },
      { No: 2, name: '李四', age: 25, city: '啊', tel: '12222323', show: true },
      {
        No: 3,
        name: '王五',
        age: 26,
        city: '广23 ',
        tel: '1233333',
        show: true
      },
      {
        No: 4,
        name: '赵二',
        age: 27,
        city: '广州asd',
        tel: '1231454523',
        show: true
      }
    ])
    return { columnList, testDatas }
  }
})
</script>
<style scoped></style>
