<template>
  <div class="home">
    <div class="nav-bar">首页</div>
    <scroll
      class="content"
      ref="scroll"
      :probeType="3"
      @scroll="contentScroll"
      @pullingUp="loadMore"
      :pullUpLoad="true"
    >
      <div v-for="(item,index) in mydata" :key="index">
        <P>{{item.name}}</P>
      </div>
    </scroll>
    <BTbutton class="back-top" @click.native="backTop" v-show="isShow" />
  </div>
</template>

<script>
import Scroll from "./scroll/Scroll";
import BTbutton from "./backTopbutton/BTbutton";
import { newData } from "./data/mydata";

export default {
  name: "navlist",
  data() {
    return {
      isShow: false,
      mydata: newData
    };
  },
  components: {
    Scroll,
    BTbutton
  },
  methods: {
    btnClick() {
      console.log("click触发了");
    },
    backClick() {
      console.log(this.$refs.backTop.scroll);
      this.$refs.scroll.scroll.scrollTo(0, 0, 3000);
    },
    backTop() {
      // 回到顶部
      // this.$refs.backTop.scroll.scrollTo(0, 0, 300);
      this.$refs.scroll.scrollTo(0, 0, 500);
    },
    contentScroll(position) {
      //  如果position.y大于1000则显示回到顶部按钮(BTbutton组件)
      this.isShow = -position.y > 1000;
    },
    loadMore() {
      const moreData = [
        {
          name: "ssssssssssssssssss"
        },
        {
          name: "nnnnnnnnnnnnnnnnnn"
        },
        {
          name: "ssssssssssssssssss"
        },
        {
          name: "nnnnnnnnnnnnnnnnnn"
        },
        {
          name: "ssssssssssssssssss"
        },
        {
          name: "nnnnnnnnnnnnnnnnnn"
        },
        {
          name: "ssssssssssssssssss"
        },
        {
          name: "nnnnnnnnnnnnnnnnnn"
        }
      ];
      // 判断图片是否加载完成，完成以后在重新刷新可滚动的距离
      // this.$refs.scroll.scroll.refresh();
      setTimeout(() => {
        this.mydata.push(...moreData);
        console.log("loadMore");
      }, 1000);
      this.$refs.scroll.finishPullUp();
    }
  }
};
</script>

<style>
.home {
  background-color: yellowgreen;
  height: 430px;
  position: relative;
}
.nav-bar {
  height: 44px;
  width: 100%;
  background-color: pink;
  text-align: center;
  line-height: 44px;
  border-bottom: 8px solid #fff;
  position: fixed;
  z-index: 9;
}
</style>