<template>
  <div class="app-container">
    <el-form :inline="true" ref="form" label-width="50px">
      <el-form-item label="分类">
        <el-input
          type="text"
          placeholder="请输入内容"
          v-model="text"
          maxlength="10"
          show-word-limit
        ></el-input>
      </el-form-item>
      <el-form-item label="详情">
        <el-input
          type="textarea"
          placeholder="请输入内容"
          v-model="textarea"
          maxlength="30"
          show-word-limit
        ></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary">添加分类</el-button>
      </el-form-item>
    </el-form>
    <br>
    <el-table
      v-loading="listLoading"
      :data="list"
      element-loading-text="Loading"
      border
      fit
      highlight-current-row
      max-height="500"
    >
      <el-table-column align="center" label="ID" width="95">
        <template slot-scope="scope">
          {{ scope.$index }}
        </template>
      </el-table-column>
      <el-table-column label="分类" width="110" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="详情">
        <template slot-scope="scope">
          {{ scope.row.title }}
        </template>
      </el-table-column>
      <el-table-column label="使用量" width="110" align="center">
        <template slot-scope="scope">
          {{ scope.row.pageviews }}
        </template>
      </el-table-column>
      <el-table-column label="操作" width="220">
        <template slot-scope="scope">
          <el-button
            size="mini"
            @click="dialogFormVisible = true">编辑</el-button>
          <el-button
            size="mini"
            type="danger"
            @click="open(scope.$index, scope.row)">删除</el-button>
            <el-button
            size="mini"
            type="info"><router‐link to="/category/details">查看</router‐link></el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog title="编辑标签" :visible.sync="dialogFormVisible">
      <el-form ref="form" label-width="50px">
        <el-form-item label="分类">
          <el-input
            type="text"
            placeholder="请输入内容"
            v-model="text"
            maxlength="10"
            show-word-limit
          ></el-input>
        </el-form-item>
        <el-form-item label="详情">
          <el-input
            type="textarea"
            placeholder="请输入内容"
            v-model="textarea"
            maxlength="30"
            show-word-limit
          ></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary">更新分类</el-button>
        </el-form-item>
      </el-form>
    </el-dialog>
  </div>
</template>

<script>
import { getList } from '@/api/table'

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'gray',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      list: null,
      listLoading: true,
      dialogFormVisible: false
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      this.listLoading = true
      getList().then(response => {
        this.list = response.data.items
        this.listLoading = false
      })
    },
    open() {
        this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$message({
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      }
  }
}
</script>
