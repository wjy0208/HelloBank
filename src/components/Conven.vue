<template>
  <div>
    <van-nav-bar title="社区支行详情页" left-text="返回" left-arrow>
      <van-icon name="ellipsis" slot="right" />
    </van-nav-bar>
    <div>
      <van-row>
        <van-col span="24"  @load="onLoad">
          <van-swipe :autoplay="3000">
            <van-swipe-item v-for="(item,index) in HxList" :key="index">
              <img :src="item.imgSrc" class="bank_bg">
            </van-swipe-item>
          </van-swipe>
        </van-col>
      </van-row>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import { Swipe, SwipeItem } from "vant";

Vue.use(Swipe).use(SwipeItem);
export default {
  data() {
    return {
      HxList: []
    }
  },
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      var that = this;
      this.$ajax.jsonData("hxbank").then(res => {
        that.HxList = res;
        console.log(that.HxList);
      });
    },
    onRefresh() {
      setTimeout(() => {
        // this.$toast("刷新成功");
        this.getData()
      }, 500)
    },
    onLoad() {
      // 异步更新数据
      setTimeout(() => {
        this.HxList = this.HxList.concat(this.HxList);
       
      }, 500)
    }
  }
};
</script>

<style scoped>
.van-nav-bar {
  background: #000;
  height: 50px;
}
.van-nav-bar__text,
.van-nav-bar .van-icon,
.van-nav-bar__title.van-ellipsis {
  color: #fff;
}
.van-nav-bar__title.van-ellipsis {
  text-align: center;
  padding-top: 5px;
  font-size: 16px;
}
</style>