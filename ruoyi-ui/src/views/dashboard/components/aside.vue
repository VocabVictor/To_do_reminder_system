<template>
  <el-container class="container">
    <el-header>
      <el-row>
        <el-col :span="21">
          我的任务
        </el-col>
        <el-col :span="2">
          <el-button icon="el-icon-plus" type="text" @click="plus"></el-button>
        </el-col>
        <el-col :span="1">
          <el-button icon="el-icon-more" type="text" @click="more"></el-button>
        </el-col>
      </el-row>
    </el-header>
    <el-main>
      <el-collapse v-model="activeNames" @change="handleChange">
        <el-collapse-item v-for="(item,index) in items" :key="index" :name="item.name" :title="item.title">
          <el-row>
            <el-col :span="4">1</el-col>
            <el-col :span="6">2</el-col>
            <el-col :span="6">3</el-col>
            <el-col :span="6">4</el-col>
            <el-col :span="2">5</el-col>
          </el-row>
        </el-collapse-item>
      </el-collapse>
    </el-main>
  </el-container>
</template>
<script>
export default {
  data() {
    return {
      activeNames: ['1'],
      items: [
        {
          title: '今天',
          name: '1'
        },
        {
          title: '明天',
          name: '2'
        },
        {
          title: '本周',
          name: '3'
        },
        {
          title: '本月',
          name: '4'
        },
        {
          title: '已延期',
          name: '5'
        },
        {
          title: '其他',
          name: '6'
        }
      ]
    }
  },
  methods: {
    handleChange(val) {
      console.log(val)
    }
  }
}
</script>

<style scoped>

.el-header {
  height: 8% !important;
  padding: 0;
}

.el-main {
  padding: 0;
}

.el-header .el-row {
  flex-grow: 1;
  width: 100%;
}


</style>
