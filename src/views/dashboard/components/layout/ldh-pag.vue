<template>
  <ElPagination
    background
    prev-text="上一页"
    next-text="下一页"
    :current-page.sync="pagination.pageNo"
    :page-sizes="[5, 10, 15, 30, 50]"
    :page-size="pagination.pageSize"
    layout="prev, pager, next, sizes, total"
    :total="pagination.total"
    @size-change="handleSizeChange"
    @current-change="handleCurrentChange"
  />
</template>

<script>
export default {
  props: {
    pagination: {
      type: Object,
      default: () => {
        return {
          pageNo: 1,
          pageSize: 10,
          total: 0,
        }
      },
    },
  },
  methods: {
    handleSizeChange(size) {
      this.$emit('size-change', size)
    },
    handleCurrentChange() {},
  },
}
</script>
