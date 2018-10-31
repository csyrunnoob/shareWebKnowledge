element Table组件简单封装(根据业务扩展)
```
<template>
  <div>
    <el-table
      :data="tableData"
      @selection-change = "handleSelectionChange"
      @expand-change = "handleExpandChange"
      empty-text='---'
    >
      <!-- 是否多选 -->
      <el-table-column
        type="selection"
        width="55"
        v-if="ifHaveCheckBox">
      </el-table-column>
      <!-- 是否展开 -->
      <el-table-column
        width="55"
        type="expand"
        v-if='ifIsExpand'>
        <template slot-scope="props">
          <!-- 展开内容 -->
          <slot></slot>
        </template>
      </el-table-column>
      <!-- table数据 -->
      <el-table-column
        v-for = '(item,index) in column'
        :key = 'index'
        :label='item.label'
        align='center'>
        <template slot-scope="scope">
          <span v-if="scope.row[item.key]===undefined||scope.row[item.key]===null||scope.row[item.key]===''||scope.row[item.key].toString().trim()==''">--</span>
          <el-popover
            placement="top"
            trigger="hover"
            v-else-if='scope.row[item.key].toString().trim().length>showLen&&showLen>0&&showLen!=0'
            :content="scope.row[item.key].toString()">
            <span slot="reference">{{ `${scope.row[item.key].toString().trim().slice(0,showLen)}...` }}</span>
          </el-popover>
          <span v-else>{{ scope.row[item.key] }}</span>
        </template>
      </el-table-column>
      <!-- 修改删除操作 -->
      <el-table-column
        label='操作'
        align='center'
        v-if='isHaveEdit||isHaveDelete'>
        <template slot-scope="scope">
          <i class="el-icon-edit pointer" v-if='isHaveEdit' @click='editHandle(scope)'></i>
          <i class="el-icon-delete pointer" v-if='isHaveDelete' @click='deleteHandle(scope)'></i>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
/**
 * @param {tableData} 表格数据
 * @param {column} 表格头数据{key:'',label:''} key代表唯一ID值,label代表名称
 * @param {showLen} 表格内容显示多长(超过改长度的显示...)
 * @param {isHaveEdit} 是否有修改
 * @function editHandle(scope) 修改事件,scope为修改行数据
 * @param {isHaveDelete} 是否有删除
 * @function deleteHandle(scope) 删除事件,scope为删除行数据
 * @param {ifHaveCheckBox} 是否显示多选
 * @function handleSelectionChange(val) val为选中项数据
 * @param {ifIsExpand} 是否可以展开
 * @function handleExpandChange(val) val为展开项数据
 */
export default {
  name: "hyTable",
  props: {
    tableData: {
      type: Array,
      default() {
        return []
      }
    },
    column: {
      type: Array,
      default() {
        return []
      }
    },
    isHaveEdit: {
      type: Boolean,
      default() {
        return false
      }
    },
    isHaveDelete: {
      type: Boolean,
      default() {
        return false
      }
    },
    showLen: {
      type: Number,
      default() {
        return 0
      }
    },
    ifHaveCheckBox: {
      type: Boolean,
      default() {
        return false
      }
    },
    ifIsExpand: {
      type: Boolean,
      default() {
        return false
      }
    }
  },
  data() {
    return {}
  },
  methods: {
    editHandle(scope) {
      this.$emit('editHandle', scope)
    },
    deleteHandle(scope) {
      this.$emit('deleteHandle', scope)
    },
    handleSelectionChange(val) {
      this.$emit('handleSelectionChange', val)
    },
    handleExpandChange(val) {
      this.$emit('handleExpandChange', val)
    }
  }
};
</script>

<style scoped>
.pointer{
  cursor: pointer;
}
.el-icon-edit,.el-icon-delete{
  margin: 0 3px;
}
</style>

```