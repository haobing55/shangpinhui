<template>
  <div>
    
    <header class="header">
      <!-- 头部的第一行 -->
      <div class="top">
        <div class="container">
          <div class="loginList">
            <p>尚品汇欢迎您！</p>
            <p v-if="!userName">
              <span>请</span>


              <!-- <a href="###">登录</a> -->
              <router-link to="/login">登录</router-link>

              <!-- <a href="###" class="register">免费注册</a> -->
              <router-link class="register" to="/register">免费注册</router-link>
            </p>
            <p v-else>
              <a>{{userName}}</a>
              <a class="register" @click="logout">退出登录</a>
              </p>
          </div>
          <div class="typeList">
            <!-- <a href="###">我的订单</a> -->
            <router-link to="/center/myorder">我的订单</router-link>
            <router-link to="/shopcart">我的购物车</router-link>
            <!-- <a href="###">我的购物车</a> -->
            <a href="###">我的尚品汇</a>
            <a href="###">尚品汇会员</a>
            <a href="###">企业采购</a>
            <a href="###">关注尚品汇</a>
            <a href="###">合作招商</a>
            <a href="###">商家后台</a>
          </div> 
        </div>
      </div>
      <!--头部第二行 搜索区域-->
      <div class="bottom">
        <h1 class="logoArea">
          <!-- <a class="logo" title="尚品汇" href="###" target="_blank">
            <img src="./images/logo.png" alt="" />
          </a> -->

          <!-- target打开新页面 -->
          <router-link class="logo" title="尚品汇" to="/home" >
            <img src="./images/logo.png" alt="" />
          </router-link>
        </h1>
        <div class="searchArea">
          <form action="" class="searchForm">
            <input
              type="text"
              id="autocomplete"
              class="input-error input-xxlarge"
              v-model="keyword"
              @keyup.enter="goSearchKeyup"
            />
            <button class="sui-btn btn-xlarge btn-danger" type="button" @click="goSearch" >
              搜索
            </button>
          </form>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name:'',
  computed:{
    userName(){
      
      return this.$store.state.user.userInfo.name
         
    }
  },
  data() {
    return {
      keyword:''
    }
  },
  mounted() {
    this.$bus.$on("clear",()=>{
      this.keyword=""
    })
  },
  methods: {
    async logout(){
      try {
        await this.$store.dispatch('userLogout')
      this.$router.push('/home')
      } catch (error) {
        alert(error)
      } 
    },
    goSearchKeyup(){
      let location={
        name:'search',
        params:{keyword:this.keyword||undefined},
      }
      if(this.$route.query){
        location.query=this.$route.query
      }
      this.$router.push(location)
    },
    goSearch(){
      //模板字符串形式传参，在input双向绑定keyword传进来，注意，params需要在路由中占位
      //this.$router.push(`/search/${this.keyword}?k=${this.keyword.toUpperCase()}`)
      //对象形式
      let location={
        name:'search',
        params:{keyword:this.keyword||undefined},
      }
      if(this.$route.query){
        location.query=this.$route.query
      }
      this.$router.push(location)
      // this.$router.push({
      //   name:'search',//在路由里声明名字，不可以用path写法，用path不会跳转路由
      //   params:{keyword:this.keyword},//此时的keyword必须在路由占位里声明同样的名字keyword,否则接收不到
      //   query:{k:this.keyword.toUpperCase()},
      // },
      // ()=>{},
      // ()=>{}//因为push和replace会返回一个promise对象,重新封装push/replace就可以解决
      
      //)
      
    }
  },
};
</script>

<style scoped lang='less'>
.header {
  & > .top {
    background-color: #eaeaea;
    height: 30px;
    line-height: 30px;

    .container {
      width: 1200px;
      margin: 0 auto;
      overflow: hidden;

      .loginList {
        float: left;

        p {
          float: left;
          margin-right: 10px;

          .register {
            border-left: 1px solid #b3aeae;
            padding: 0 5px;
            margin-left: 5px;
          }
        }
      }

      .typeList {
        float: right;

        a {
          padding: 0 10px;

          & + a {
            border-left: 1px solid #b3aeae;
          }
        }
      }
    }
  }

  & > .bottom {
    width: 1200px;
    margin: 0 auto;
    overflow: hidden;

    .logoArea {
      float: left;

      .logo {
        img {
          width: 175px;
          margin: 25px 45px;
        }
      }
    }

    .searchArea {
      float: right;
      margin-top: 35px;

      .searchForm {
        overflow: hidden;

        input {
          box-sizing: border-box;
          width: 490px;
          height: 32px;
          padding: 0px 4px;
          border: 2px solid #ea4a36;
          float: left;

          &:focus {
            outline: none;
          }
        }

        button {
          height: 32px;
          width: 68px;
          background-color: #ea4a36;
          border: none;
          color: #fff;
          float: left;
          cursor: pointer;

          &:focus {
            outline: none;
          }
        }
      }
    }
  }
}
</style>