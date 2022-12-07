<template>
  <el-container class="container">
     <mymain></mymain>
  </el-container>
</template>

<script>
import mymain from '@/views/items/components/main'
export default {
  name: 'dashboard',
  components: {
    mymain
  }
}
</script>

<style scoped>
  .container{
    width: 100%;
    height: 100%;
    padding: 10px;

  }
  .el-aside{
    width: 59%!important;
    height: 100%;
    margin-right: 1%;
  }
  .el-header{
    height: 49%!important;
    margin-bottom: 2%;
  }

  .el-header,.el-aside,.el-main{
    border:1px solid #ddd;
    border-radius: 4px;
  }

</style>
