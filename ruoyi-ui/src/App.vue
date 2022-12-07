<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>

export default {
  name: "App",
  metaInfo() {
    return {
        title: this.$store.state.settings.dynamicTitle && this.$store.state.settings.title,
        titleTemplate: title => {
            return title ? `${title} - ${process.env.VUE_APP_TITLE}` : process.env.VUE_APP_TITLE
        }
    }
  }
};
</script>
<style >
#app{
  background-color: #FAFAFA;
}
.el-col{
  color: #333!important;
}

.container{
  width: 100%;
  height: 100%;
  padding: 6px!important;
}
button i{
  color:#606266;
}
.el-header{
  display: flex;
  align-items: center;
}

.el-aside,.el-main,.el-header{
  background-color: white;
}
</style>
