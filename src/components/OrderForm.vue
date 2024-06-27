<template>
    <div class="order-form">
      <header>
        <span class="toProfile" @click="toCart">
            <i class="el-icon-arrow-left" ></i>
        </span>
        <h3>オーダー</h3>
      </header>
      <main>
        <div class="order-form-item">
          <div v-for="item in cartGoods" v-if="cartGoods.length > 0" class="goods">
            <div class="left">
              <img :src="item.img">
            </div>
            <div class="right">
              <p>{{ item.count }}</p>
            </div>
          </div>
        </div>
        <div class="order-form-item">
          <p>合計：
            <span class="price">￥{{ pay }}</span>
          </p>
        </div>
        <div class="order-form-item">
          <span>住所：</span>
            <el-select v-model="selectAddress" :placeholder="addressPlaceHolder" v-if="address.length > 0">
              <el-option
                v-for="(item,index) in address"
                :key="index"
                :label="item.name + item.phone + item.city + item.detailAdd"
                :value="index"
                >
              </el-option>
            </el-select>

        </div>
      </main>
      <footer class="order-form-footer">
        <div>
            <span class="price-wrap">支払<span class="price">￥{{ pay }}</span></span>
            <el-button type="danger" class="text-right" @click="toPay">支払いへ<i class="el-icon-arrow-right el-icon--right"></i></el-button>
        </div>
      </footer>
    </div>
</template>

<script>
export default {
  data() {
    return {
      addressPlaceHolder: '届け先を選択してください',
      selectAddress: 0
    }
  },
  computed: {
    cartGoods () {
      return this.$route.query.cartGoods;
    },
    pay () {
      return this.$route.query.pay;
    },
    address () {
      return this.$store.state.address;
    }
  },
  methods: {
    toCart () {
      this.$router.push({
        path: '/Cart'
      })
      this.$store.state.cartCounter++;
      this.$store.state.cartCounter--;
    },
    toPay () {
      this.$store.state.cartGoods = [];
      this.$store.state.cartCounter = 0;
      this.$router.push({
        path: '/Cart'
      })
      //解决主页与详情页切换时，菜单栏无法更新获取当前路由的问题
      this.$store.state.cartCounter++;
      this.$store.state.cartCounter--;
      alert('支払い完成！');
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/css/variable.scss";

.order-form{
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
    margin-top: 10px;
    text-align: left;
    .order-form-item{
      padding: 10px;
      background-color: #fff;
      margin-top: 10px;
    }
    .goods{
      height: 40px;
      line-height: 40px;
      border-bottom: 1px solid #eee;
      clear: both;
      .left{
        float: left;
        height: 100%;
        img{
          height: 100%;
        }
      }
      .right{
        float: right;
      }
    }
    .address{
    }
    .price{
      color: $mainRed;
      font-size: 18px;
      font-weight: 600;
      float: right;
    }
  }
  .order-form-footer{
    position: fixed;
    width: 100%;
    height: $cartFooterHeight;
    line-height: $cartFooterHeight;
    bottom: 0;
    border-top: 1px solid #eee;
    left: 0;
    text-align: right;
    background-color: #fff;
    .price-wrap{
      float: left;
      padding-left: 10px;
      font-size: 18px;
    }
    .price{
      color: $mainRed;
      font-weight: 600;
    }
  }
  .el-button--danger{
    background-color: $mainRed;
    border: none;
    border-radius: 0;
  }
}
</style>