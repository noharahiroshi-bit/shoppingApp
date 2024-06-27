<template>
  <div class="login-page">
    <header>
      <span class="toPrePage" @click="toPrePage">
          <i class="el-icon-arrow-left" ></i>
      </span>
      <h3>ログイン</h3>
    </header>
    <main>
      <div class="login">
        <el-form>
          <el-form-item>
            <el-input v-model="username" placeholder="アカウントを入力してください"></el-input>
          </el-form-item>
          <el-form-item>
            <el-input type="password" v-model="password" placeholder="パスワードを入力してください"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="success" @click="login">ログイン</el-button>
            <el-button>アカウントを作る</el-button>
          </el-form-item>
        </el-form>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    return {
      username: '佐藤',
      password: '123456',
    }
  },
  methods: {
    login () {
      this.$store.commit('login', this.username);
      this.$router.go(-1);
    },
    toPrePage () {
      this.$router.go(-1);
    }
  }
}
</script>

<style lang="scss" scoped>
.login-page{
  width: 100%;
  height: 100%;
  background-color: #fff;
  position: relative;
  z-index: 1001;
  header{
    position: relative;
    height: 50px;
    line-height: 50px;
    .toPrePage i{
      position: absolute;
      left: 10px;
      font-size: 20px;
      top: 50%;
      transform: translateY(-50%);
    }
  }
  main{
    width: 80%;
    position: absolute;
    top: 50%;
    left: 10%;
    transform: translateY(-50%);
  }

}

</style>
