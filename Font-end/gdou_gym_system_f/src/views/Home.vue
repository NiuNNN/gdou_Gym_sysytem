<template>
  <el-container class="home-container">
    <el-header style="height: 80px;" v-if="isRouterAlive"><Navbar></Navbar></el-header>
    <el-container>
      <el-aside width="200px"><Aside></Aside></el-aside>
      <el-main>
        <router-view v-if="isRouterAlive"></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import Navbar from '@/components/navbar.vue'
import Aside from '@/components/aside.vue'
export default {
  provide(){
    return {
        reload: this.reload
    };
  },
  data() {
    return {
      isRouterAlive:true
    }
  },
  components:{
    Navbar,
    Aside
  },
  methods:{
     reload() {
        this.isRouterAlive = false;
        this.$nextTick(function () {
            this.isRouterAlive = true;
        });
    }
  }
}
</script>

<style lang="less" scoped>
.home-container {
  height: 100%;
  width: 80%;
  // background-color: pink;
  margin: 0 auto;
}
</style>