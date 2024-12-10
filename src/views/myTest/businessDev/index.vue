<template>
  <lay-panel>
    <lay-button>默认按钮</lay-button>
    <lay-button type="primary">原始按钮</lay-button>
    <lay-button type="normal">百搭按钮</lay-button>
    <lay-button type="warm">暖色按钮</lay-button>
    <lay-button type="danger">警告按钮</lay-button>
  </lay-panel>

  <base-table></base-table>

</template>

<script>
import baseTable from '@/components/BaseTable/index.vue'
export default {
  components: {
    baseTable, // 注册组件
  },
  data() {
    return {

    }
  },
  mounted() {
  },
  methods: {

  }
}
</script>
