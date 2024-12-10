<template>
  <lay-table
      :page="table.page"
      :columns="table.columns"
      :loading="table.loading"
      :data-source="table.data"
      :default-toolbar="true"
      skin="line"
  ></lay-table>
  <lay-page v-model="table.currentPage" :limit="table.size" :total="table.total" :layout="table.layout"
            theme="blue" @change="loadTableData">
  </lay-page>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      table: {
        columns: [
          {key: 'id', title: "id", align: "left", ellipsisTooltip: true, width: 150},
          {key: 'name', title: "姓名", align: "left", ellipsisTooltip: true, width: 150},
        ],
        data: [{id:1,name:'张三'},{id:2,name:'李四'}],
        loading: false,
        page: 1,
        size: 10,
        total: 0,
        layout: ["prev", "page", "next", "skip", "count", "limits"]
      }
    }
  },
  methods: {
    loadTableData({current, limit}) {
      this.table.loading = true;
      // axios.get('/admin/MyTest/testApi', {
      axios.get('', {
        params: {
          page: current,
          limit: limit,
          ...this.form,
        }
      }).then((res) => {
        this.table.data = res.data.data || [];
        this.table.total = res.data.count || 0;
        this.table.currentPage = current;
        this.table.size = limit;
      }).finally(() => {
        this.table.loading = false;
      });
    },
    search() {
      // 重置分页参数到第一页，并加载数据
      this.table.currentPage = 1;
      this.loadTableData({
        current: this.table.currentPage,
        limit: this.table.size,
      });
    },
    handlePageChange(newPage) {
      this.loadTableData({
        current: newPage,
        limit: this.table.size,
      });
    },
    handlePageSizeChange(newSize) {
      this.table.size = newSize;
      this.table.currentPage = 1; // 切换每页数量时回到第一页
      this.loadTableData({
        current: this.table.currentPage,
        limit: newSize,
      });
    },
  }
}
</script>

<style scoped lang="scss">
.layui-table-tool td {
  background-color: #ffffff !important; /* 背景颜色 */
  border: 1px solid #ffffff; /* 可选：调整边框颜色 */
  color: #333333; /* 可选：调整字体颜色 */
}
:deep(.layui-table-header th) {
  background-color: #ffffff !important; /* 白色背景 */
  color: #333333; /* 字体颜色 */
}
</style>