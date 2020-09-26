<template>
  <div class="CustomerList">
    <!-- <div
      class="item acea-row row-between-wrapper"
      v-for="(item, index) in list"
      :key="index"
    >
      联系客服(telegram):
      <a class="money font-color-red" :href="'tg://resolve?domain=' + item">
        {{ item }}</a
      >
      <span class="copy" :data-clipboard-text="item"> 复制</span>
    </div> -->
     <div
      class="item acea-row row-between-wrapper"
    >
      联系客服(telegram):
      <a class="money font-color-red" href="https://t.me/love124com6">
        https://t.me/love124com6</a
      >
      <span class="copy" :data-clipboard-text="item"> 复制</span>
    </div>
    <!-- <div
      class="item acea-row row-between-wrapper"
      v-for="item in list"
      :key="item.id"
      @click="
        $router.push(
          '/customer/chat/' +
            item.uid +
            '/' +
            productId +
            (orderId ? '?orderId=' + orderId : '')
        )
      "
    >
      <div class="pictrue"><img :src="item.avatar" /></div>
      <div class="text line1">{{ item.nickname }}</div>
    </div> -->
  </div>
</template>
<script>
import { serviceList } from "@api/user";
import ClipboardJS from "clipboard";

export default {
  name: "CustomerList",
  data() {
    return {
      list: [],
      productId: 0,
      orderId: ""
    };
  },
  watch: {
    $route(n) {
      if (n.name === "CustomerList") {
        if (n.params.productId) this.productId = n.params.productId;
        else this.productId = 0;

        if (n.query.orderId) this.orderId = n.query.orderId;
        else this.orderId = "";
      }
    }
  },
  methods: {
    getList() {
      serviceList().then(res => {
        this.list = res.data;
      });
    }
  },
  mounted() {
    this.getList();
    if (this.$route.params.productId)
      this.productId = this.$route.params.productId;
    if (this.$route.query.orderId) this.orderId = this.$route.query.orderId;
    this.$nextTick(function() {
      let copybtn = document.getElementsByClassName("copy");
      const clipboard = new ClipboardJS(copybtn);
      clipboard.on("success", () => {
        this.$dialog.success("复制成功");
      });
    });
  }
};
</script>
<style scoped>
.CustomerList {
  margin-top: 0.13rem;
}
.CustomerList .item {
  height: 1.38rem;
  border-bottom: 1px solid #eee;
  padding: 0 0.24rem;
  background-color: #fff;
}
.CustomerList .item .pictrue {
  width: 0.9rem;
  height: 0.9rem;
  border-radius: 50%;
  border: 0.03rem solid #fff;
  box-shadow: 0 0 0.1rem 0.05rem #f3f3f3;
  -webkit-box-shadow: 0 0 0.1rem 0.05rem #f3f3f3;
  -moz-box-shadow: 0 0 0.1rem 0.05rem #f3f3f3;
}
.CustomerList .item .pictrue img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
}
.CustomerList .item .text {
  width: 5.82rem;
  font-size: 0.32rem;
  color: #000;
}
.money {
  flex: 1;
  text-align: right;
}
.copy {
  font-size: 0.14rem;
  border: 0.01rem solid #1d9cb1;
  border-radius: 0.04rem;
  color: #1d9cb1;
  margin-left: 0.05rem;
  padding: 0.03rem;
  cursor: pointer;
}
</style>
