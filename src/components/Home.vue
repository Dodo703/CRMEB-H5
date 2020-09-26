<template>
  <div
    class="home"
    :style="{ bottom: bottom + 'px' }"
    style="position:fixed;"
    id="right-nav"
    @touchmove="touchmove($event)"
  >
    <div class="homeCon bg-color-red" :class="homeActive === true ? 'on' : ''">
      <router-link
        :to="'/customer/list'"
        class="iconfont icon-kefu"
      ></router-link>
      <router-link
        :to="'/'"
        class="iconfont icon-shouye-xianxing"
      ></router-link>
      <router-link
        :to="'/cart'"
        class="iconfont icon-caigou-xianxing"
      ></router-link>
      <router-link :to="'/user'" class="iconfont icon-yonghu1"></router-link>
    </div>
    <div class="pictrue" @click="open">
      <img
        :src="
          homeActive === true
            ? require('../assets/images/close.gif')
            : require('../assets/images/open.gif')
        "
        class="image"
      />
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
export default {
  name: "Home",
  props: {},
  data: function() {
    return {
      top: "",
      bottom: ""
    };
  },
  computed: mapGetters(["homeActive"]),
  methods: {
    touchmove(event) {
      this.bottom = "auto";
      event.preventDefault();
      let bottom =
        document.body.clientHeight -
        (event.touches[0].pageY -
          (document.documentElement.scrollTop || document.body.scrollTop) -
          this.$el.clientHeight);

      if (bottom > 390) bottom = 390;
      else if (bottom < 80) bottom = 80;
      this.bottom = bottom;
    },
    open: function() {
      this.homeActive
        ? this.$store.commit("CLOSE_HOME")
        : this.$store.commit("OPEN_HOME");
    }
  },
  created() {
    this.bottom = "50px";
  }
};
</script>

<style scoped>
.pictrueBox {
  width: 1.3rem;
  height: 1.2rem;
}
</style>
