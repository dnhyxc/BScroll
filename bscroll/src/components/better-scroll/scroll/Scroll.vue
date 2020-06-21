<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll';
export default {
  name: "Scroll",
  data() {
    return {
      scroll: null,
    };
  },
  props: {
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  mounted() {
    this.scroll = new BScroll(this.$refs.wrapper, {
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad
    });
    this.scroll.on("scroll", position => {
      // console.log(position);
      this.$emit("scroll", position);
    });
    this.scroll.on("pullingUp", () => {
      // console.log("上拉加载更多");
      // setTimeout(() => {
      //   this.scroll.finishPullUp();
      // }, 2000);
      this.$emit('pullingUp')
    });
  },
  methods: {
    scrollTo(x, y, time = 300) {
      this.scroll.scrollTo(x, y, time);
    },
    finishPullUp(){
       this.scroll.finishPullUp()
    }
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
.wrapper {
  background-color: #4c4c4c;
  /* calc()该方法用于计算宽高样式属性 */
  height: calc(100% - 100px);
  padding-top: 44px;
}
.content {
  text-align: center;
  width: calc(100%-10px);
  overflow: hidden;
  padding-top: 51px;
}
</style>