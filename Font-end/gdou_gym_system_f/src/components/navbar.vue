<template>
  <div class="header-container">
    <div class="logo">
      <span>广东海洋大学体育馆管理平台</span>
    </div>
    <div class="userinfo">
      <img :src="imgUrl" alt="">
      <span style="font-size:13px">欢迎回来，{{ username }}</span>
      <el-button type="primary" plain @click="loginout">退出</el-button>
    </div>
  </div>
</template>

<script>
import request from '@/utils/request.js'
export default {
  inject:['reload'],
  data() {
    return {
      imgUrl:'',
    }
  },
  created(){
    this.getImgUrl()
  },
  computed:{
    username(){
      let name = localStorage.getItem('username')
      let userclass = localStorage.getItem('userclass')
      let username;
      if(userclass === "user"){
        username = name+" 同学"
      }
      else{
        username = name+" 管理员" 
      }
      return username
    }
  },
  methods: {
    loginout(){
      this.$confirm("此操作为退出登录，是否继续？","提示",{type:"info"}).then(res=>{
        localStorage.removeItem('userid')
        localStorage.removeItem('username');
        localStorage.removeItem('Authorization');
        localStorage.removeItem('signTime');
        localStorage.removeItem('userclass')
        this.$router.push('/user_login');
      })
    },
    getImgUrl(){
      let userid = localStorage.getItem('userid')
      this.imgUrl="http://localhost/avatar/"+userid+".jpg"+"?"+Math.random()*10
      console.log(this.imgUrl);
    }
  },
}
</script>

<style lang="less" scoped>
.header-container{
  position: absolute;
  width: 80%;
  height: 79px;
  border-bottom: 1px solid #dcdfe6;
  .logo{
    display: inline-block;
    span{
      height: 79px;
      color: #409eff;
      line-height: 79px;
      font-size: 30px;
      font-weight: 700;
      padding-left: 15px;
    }
  }
  .userinfo{
    z-index: 999;
    height: 79px;
    display: inline-block;
    float: right;
    margin-right: 15px;
    color: #888;
    .el-button{
      margin-left: 30px;
    }
  }
  img{
    position: relative;
    top: 18px;
    right: 14px;
    width: 60px;
    height: 60px;
    border-radius: 50%;
  }
}
</style>