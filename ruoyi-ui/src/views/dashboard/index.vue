<template>
  <el-container class="container">
    <el-aside>
      <myaside></myaside>
    </el-aside>
    <el-container>
      <el-header>
        <myheader></myheader>
      </el-header>
      <el-main><mymain></mymain></el-main>
    </el-container>
  </el-container>
</template>

<script>
import myaside from '@/views/dashboard/components/aside'
import myheader from '@/views/dashboard/components/header'
import mymain from '@/views/dashboard/components/main'
export default {
  name: 'dashboard',
  components: {
    myaside, myheader, mymain
  }
}
</script>

<style scoped>
.el-aside {
  width: 59% !important;
  height: 100%;
  margin-right: 1%;
  padding: 24px;
}

.el-header {
  height: 49% !important;
  margin-bottom: 2%;
}

.el-header, .el-aside, .el-main {
  border: 1px solid #ddd;
  border-radius: 4px;
}

.el-row, .el-col {
  display: flex;
  align-items: center;
  height: 100%;
}

.el-row {
  justify-content: center;
}
</style>
