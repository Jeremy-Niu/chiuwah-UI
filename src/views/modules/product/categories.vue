<
<template>
  <el-container style="height: 800px; border: 1px solid #eee">
    <el-aside width="250px" style="background-color: rgb(238, 241, 246)">
      <el-table ref="menuTable" highlight-current-row :data="listMenu" stripe style="width: 100%"
                @row-dblclick="getList">
        <el-table-column ref="aside-header" prop="category" label="类型" width="220" align="left"></el-table-column>

      </el-table>
    </el-aside>
    <el-container>
      <el-header style="text-align: right; font-size: 12px">
        <el-dropdown>
          <i class="el-icon-setting" style="margin-right: 15px"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>查看</el-dropdown-item>
            <el-dropdown-item>新增</el-dropdown-item>
            <el-dropdown-item>删除</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-header>
      <el-main>
        <el-table :data="items" stripe style="width: 100%">
          <el-table-column prop="itemName" label="名称" >
          </el-table-column>
          <el-table-column prop="barcode" label="条形码" width="120">
          </el-table-column>
          <el-table-column prop="itemNum" label="商品编号">
          </el-table-column>
        </el-table>
        <el-pagination
          :page-size="20"
          :pager-count="11"
          layout="prev, pager, next"
          :total="1000">
        </el-pagination>
      </el-main>

    </el-container>

  </el-container>

</template>

<script>
export default {
  components: {},
  props: {},
  data () {
    const listMenu = []
    const items = []
    return {
      items,
      listMenu
    }
  },
  computed: {},
  watch: {},
  methods: {
    getList (row, column, cell, event) {
      const type = row.category
      this.$http({
        url: this.$http.adornUrl('/product/listbytype/' + type),
        method: 'get'
      }).then(({data}) => {
        this.items = data.data
      })
    },
    getType () {
      this.$http({
        url: this.$http.adornUrl('/category/type'),
        method: 'get'
      }).then(({data}) => {
        this.listMenu = data.data
      })
    }
  },
  beforeCreate () {
  },
  created () {
    this.getType()
  },
  beforeMount () {
  },
  mounted () {
  },
  beforeUpdate () {
  },
  updated () {
  }
}
</script>


<style>
.el-header {
  background-color: #B3C0D1;
  color: #333;
  line-height: 60px;
}

.el-aside {
  color: #333;
}
</style>
