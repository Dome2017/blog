<template>
  <div id="nav">
    <el-menu  class="el-menu-demo" mode="horizontal" router=true>
      <el-menu-item index="/">首页</el-menu-item>
      <el-menu-item index="/blog">博客</el-menu-item>
      <el-submenu class="uuu" v-if=this.$store.getters.getUser.userId>
        <template slot="title">
<!--          <el-avatar :size="40" :src="photo"></el-avatar>-->
          {{this.$store.getters.getUser.userName}}
        </template>
<!--        <el-menu-item index="2-1">我的信息</el-menu-item>-->
<!--        <el-menu-item @click="check">我的动态</el-menu-item>-->
        <el-menu-item @click="logout">退出</el-menu-item>
      </el-submenu>
      <el-menu-item v-else index="/login">登陆</el-menu-item>
    </el-menu>
    <router-view/>
  </div>
</template>
<script>
  export default {
    data() {
      return {
          drawer: false,
          innerDrawer: false,
      };
    },
    methods: {
      handleCommand(command) {
        this.$message('click on item ' + command);
      },
      logout(){
        this.$store.commit("REMOVE_INFO")
        this.status=false
      }
    },
      created() {
        if(this.$store.getters.getUser==null){
            this.$store.commit("SET_USERINFO", {userId:""})
        }
      }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.uuu{
    margin-right: 10%;
}
#nav {
  padding: 20px;
  max-width: 70vw;
  margin-left: 10vw;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}


</style>
