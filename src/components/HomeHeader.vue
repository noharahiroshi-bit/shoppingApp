<template>
  <header class="home-header">
    <h4 class="top-text"> AEHAOTA </h4>
    <div class="tap-menu">
      <el-tabs :tab-position="'top'" type="border-card" style="height: 39px;" v-model="goodsType" @tab-click="changeGoodsType">
        <el-tab-pane label="すべてを見る" name="すべてを見る"></el-tab-pane>
        <el-tab-pane label="シャツ" name="シャツ"></el-tab-pane>
        <el-tab-pane label="パンツ" name="パンツ"></el-tab-pane>
        <el-tab-pane label="ジンズ" name="ジンズ"></el-tab-pane>
        <el-tab-pane label="アクセサリー" name="アクセサリー"></el-tab-pane>
        <el-tab-pane label="シューズ" name="シューズ"></el-tab-pane>
        <el-tab-pane label="ベーシック" name="ベーシック"></el-tab-pane>
        <el-tab-pane label="靴下" name="靴下"></el-tab-pane>
      </el-tabs>
    </div>
  </header>
</template>

<script>
export default {
  name: 'home-header',
  data () {
    return {
      kindToType: new Map([
        ['すべてを見る', 0],
        ['シャツ', 1],
        ['パンツ', 2],
        ['ジンズ', 3],
        ['アクセサリー', 4],
        ['シューズ', 5],
        ['ベーシック', 6],
        ['靴下', 7]
      ]),
      goodsType: 'すべてを見る'
    }
  },
  methods: {
    changeGoodsType () {
      this.$store.state.GoodsCurrentSelKind = this.kindToType.get(this.goodsType)
    },
  },
}
</script>

<style lang="scss" scoped>
@import "../assets/css/variable.scss";

.home-header{
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  background-color: #fff;
  z-index: 999;
  .top-text{
    height: $HomeHeaderHeight - 40px;
    line-height: $HomeHeaderHeight - 40px;
  }
  .tap-menu{
  }
}
</style>
