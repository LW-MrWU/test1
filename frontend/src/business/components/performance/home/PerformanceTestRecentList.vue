<template>
  <el-card class="table-card" v-loading="result.loading">
    <template v-slot:header>
      <span class="title">{{ $t('commons.test') }}</span>
    </template>
    <el-table border :data="tableData" class="adjust-table table-content" @row-click="link" height="300px">
      <el-table-column prop="name" :label="$t('commons.name')" width="150" show-overflow-tooltip/>
      <el-table-column width="180" :label="$t('commons.create_time')">
        <template v-slot:default="scope">
          <span>{{ scope.row.createTime | timestampFormatDate }}</span>
        </template>
      </el-table-column>
      <el-table-column width="180" :label="$t('commons.update_time')">
        <template v-slot:default="scope">
          <span>{{ scope.row.updateTime | timestampFormatDate }}</span>
        </template>
      </el-table-column>
      <el-table-column prop="status" :label="$t('commons.status')">
        <template v-slot:default="{row}">
          <ms-performance-test-status :row="row"/>
        </template>
      </el-table-column>
    </el-table>
  </el-card>
</template>

<script>

import MsPerformanceTestStatus from "../test/PerformanceTestStatus";
import {getCurrentProjectID, getCurrentWorkspaceId} from "@/common/js/utils";

export default {
  name: "MsPerformanceTestRecentList",
  components: {MsPerformanceTestStatus},
  data() {
    return {
      result: {},
      tableData: []
    };
  },

  methods: {
    search() {
      let condition = {
        workspaceId: getCurrentWorkspaceId(),
        projectId: getCurrentProjectID()
      };
      this.result = this.$post("/performance/recent/5", condition, response => {
        this.tableData = response.data;
      });
    },
    link(row) {
      this.$router.push({
        path: '/performance/test/edit/' + row.id,
      });
    }
  },

  created() {
    this.search();
  },
  activated() {
    this.search();
  }
};
</script>

<style scoped>

.el-table {
  cursor: pointer;
}

</style>
