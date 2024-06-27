<template>
    <div class="add-new-address">
      <header>
        <span class="toProfile" @click="toProfile">
            <i class="el-icon-arrow-left" ></i>
        </span>
        <h3> 新しい住所を追加</h3>
      </header>
      <main>
        <el-form :model="newAddForm" :rules="rules" :label-position="'left'" ref="newAddForm" label-width="100px" class="newAddForm">
          <el-form-item label="お届け先氏名" prop="name">
            <el-input v-model="newAddForm.name"></el-input>
          </el-form-item>
          <el-form-item label="電話番号" prop="phone">
            <el-input v-model.number="newAddForm.phone"></el-input>
          </el-form-item>
          <el-form-item label="住所" prop="city">
            <el-input v-model="newAddForm.city"></el-input>
          </el-form-item>
          <el-form-item label="お届け先" prop="detailAdd">
            <el-input v-model="newAddForm.detailAdd"></el-input>
          </el-form-item>
        </el-form>
      </main>
      <footer>
        <el-form>
          <el-form-item>
            <el-button type="primary" @click="submitForm('newAddForm')">お届け先をセーブする</el-button>
            <el-button type="danger" @click="resetForm('newAddForm')">リセット</el-button>
          </el-form-item>
        </el-form>
      </footer>
    </div>
</template>

<script>
export default {
  data() {
    let validatePhone = (rule, value, callback) => {
        if (!value) {
            return callback(new Error('電話番号は必要です。'));
        } else if (!/^1[3-9]{1}[0-9]{9}$/.test(value)) {
            return callback(new Error('電話番号は正しくありません'));
        } else {
            callback();
        }
    };
    return {
      newAddForm: {
        name: '',
        phone: '',
        city: '',
        detailAdd: ''
      },
      rules: {
        name: [
          { required: true, message: '名前を入力してください', trigger: 'blur' }
        ],
        phone: [
          {required: true, validator: validatePhone, trigger: 'blur'}
        ],
        city: [
          { required: true, message: '住所を入力してください', trigger: 'blur' }
        ],
        detailAdd: [
          { required: true, message: '詳しい住所を入力してください', trigger: 'blur' }
        ],
      }
    }
  },
  methods: {
    toProfile () {
      this.$router.push({
        path: '/Profile/EditAddressPage'
      })
      //解决主页与详情页切换时，菜单栏无法更新获取当前路由的问题
      this.$store.state.cartCounter++;
      this.$store.state.cartCounter--;
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$store.commit('addNewAddress', this.newAddForm);
          this.$router.push({
            path: '/Profile/EditAddressPage'
          })
        } else {
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }

}
</script>

<style lang="scss" scoped>
@import "../assets/css/variable.scss";

.add-new-address{
  width: 100%;
  height: 100%;
  position: absolute;
  z-index: 1001;
  background-color: #f5f5f5;
  header{
    position: relative;
    height: 50px;
    line-height: 50px;
    background-color: #fff;

    .toProfile i{
      position: absolute;
      left: 10px;
      font-size: 20px;
      top: 50%;
      transform: translateY(-50%);
    }
  }
  main{
    background-color: #fff;
    margin-top: 10px;
    padding: 10px;
  }
  footer{
    margin-top: 50px;
  }
}
</style>