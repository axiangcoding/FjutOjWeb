<template>
  <!-- add by foxfox [20190812]  -->
  <div class="mall-body">
    <div class="pic-block">
      <el-carousel>
        <el-carousel-item
          v-for="item in 4"
          :key="item"
        >
          <el-image
            class="picture"
            :src="src"
            :fits="fits"
          ></el-image>
        </el-carousel-item>
      </el-carousel>
    </div>
    <el-col
      :span="4"
      v-for="(o) in dataMallInfo"
      :key="o.id"
      class="main-col"
    >
      <el-card
        class="product-card"
        shadow="hover"
        :body-style="{ padding: '0px' }"
      >
        <div
          class="product-box"
          @click="toProductDetail(o.id)"
        >
          <el-image
            src="http://www.fjutacm.com/pic/defaulthead.jpg"
            class="image"
          ></el-image>
          <div>
            <font size="4">{{o.title}}</font>
            <br />
            <font
              size="5"
              color="orange"
            >{{o.acb}}</font>ACB
          </div>
        </div>
      </el-card>
    </el-col>
  </div>

</template>

<script>
export default {
  data () {
    return {
      dataMallInfo: [],
      fits: ['scale-down'],
      src: 'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1565605041042&di=96861ed2d333564674f15042571c6497&imgtype=0&src=http%3A%2F%2Fhbimg.b0.upaiyun.com%2F73537f118ccb2540ac0a49e2cb57cd74469444c2a608a-yNTFeJ_fw658'
    }
  },
  mounted () {
    this.getMalldata()
  },
  methods: {
    toProductDetail (gid) {
      if (this.$store.getters.getIsLogin) {
        this.$router.push({ path: 'ProductDetail', query: { id: gid } })
      } else {
        this.$message.warning('登录后才能查看详情哦！')
      }
    },
    async getMalldata () {
      let dataMall = await this.$http.get('/mall/getMallGoods')
      if (dataMall.code === 100) {
        this.dataMallInfo = dataMall.datas[0]
      } else {
        this.$message.warning('没有任何商品')
      }
    }
  }

}
</script>

<style scoped>
.mall-body {
  width: 85%;
  min-height: 800px;
  margin: auto;
  background-color: #fafafa;
}

.pic-block {
  width: 85%;
  margin: auto;
}

.picture {
  height: 250px;
  width: 100%;
  margin: auto;
}

.image {
  width: 100%;
  display: block;
}

.product-main {
  width: 1400px;
  margin: 0;
}

.main-col {
  margin-left: 90px;
}

.product-card {
  cursor: pointer;
  height: 310px;
  margin-bottom: 20px;
}

.product-box {
  width: 100%;
  height: 310px;
}
</style>
