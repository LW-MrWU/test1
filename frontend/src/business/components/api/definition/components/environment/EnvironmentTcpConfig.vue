<template>
  <el-form class="tcp" :model="config" :rules="rules" ref="config" label-width="100px" :disabled="isReadOnly"
           size="small">

    <el-row :gutter="10">
      <el-col :span="16">
        <el-form-item :label="$t('api_test.request.tcp.server')" prop="server">
          <el-input v-model="config.server" maxlength="300" show-word-limit/>
        </el-form-item>
      </el-col>
      <el-col :span="8">
        <el-form-item :label="$t('api_test.request.tcp.port')" prop="port" label-width="60px">
          <el-input v-model="config.port"/>
        </el-form-item>
      </el-col>
    </el-row>

  </el-form>
</template>

<script>

export default {

  name: "EnvironmentTcpConfig",
  props: {
    config: {},
    isReadOnly: {
      type: Boolean,
      default: false
    },
  },
  data() {
    return {
      rules: {}
    }
  },
}
</script>

<style scoped>
.tcp >>> .el-input-number {
  width: 100%;
}
</style>
