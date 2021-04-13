<template>
  <div class="position">
    <span class="iconfont position__icon">&#xe64f;</span>
    xxxx大学xxxx大学xxxx大学xxxx大学xxxx大学xxxx大学
    <span class="iconfont position__notice">&#xe613;</span>
  </div>
  <div class="search">
    <span class="iconfont">&#xe61f;</span>
    <span class="search__text">商店优惠商品</span>
  </div>
  <div class="banner">
    <img
      class="banner__img"
      src="http://www.dell-lee.com/imgs/vue3/banner.jpg"
      alt=""
    />
  </div>
  <div class="icons">
    <div class="icons__item" v-for="menu in menuList" :key="menu.imgUrl">
      <img class="icons__item__img" :src="menu.imgUrl" alt="" />
      <p class="icons__item__desc">{{ menu.name }}</p>
    </div>
  </div>
  <div class="gap"></div>
</template>

<script>
export default {
  name: 'StaticPart',

  setup () {
    const menuList = [
      {
        name: '超市便利',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/超市.png'
      },
      {
        name: '菜市场',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/菜市场.png'
      },
      {
        name: '水果店',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/水果店.png'
      },
      {
        name: '鲜花绿植',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/鲜花.png'
      },
      {
        name: '医药健康',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/医药健康.png'
      },
      {
        name: '家具时尚',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/家居.png'
      },
      {
        name: '烘焙蛋糕',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/蛋糕.png'
      },
      {
        name: '签到',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/签到.png'
      },
      {
        name: '大牌免运',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/大牌免运.png'
      },
      {
        name: '红包套餐',
        imgUrl: 'http://www.dell-lee.com/imgs/vue3/红包.png'
      }
    ]
    return {
      menuList
    }
  },

  components: {},

  watch: {},

  computed: {},

  mounted () {},

  methods: {}
}
</script>

<style lang="scss" scoped>
@import '../../style/variables.scss';
@import '../../style/mixins.scss';

.position {
  position: relative;
  padding: 0.16rem 0.24rem 0.16rem 0;
  line-height: 0.22rem;
  font-size: 0.16rem;
  @include ellipsis;
  .position__icon {
    position: relative;
    top: 0.01rem;
    font-size: 0.2rem;
  }
  .position__notice {
    position: absolute;
    right: 0;
    top: 0.17rem;
    font-size: 0.2rem;
  }
  color: $content-fontcolor;
}
.search {
  margin-bottom: 0.12rem;
  line-height: 0.32rem;
  background: #f5f5f5;
  color: #b7b7b7;
  border-radius: 0.16rem;
  font-size: 0.14rem;
  .iconfont {
    position: relative;
    top: 0.02rem;
    display: inline-block;
    padding: 0 0.08rem 0 0.16rem;
    font-size: 0.18rem;
  }
  &__text {
    display: inline-block;
    font-size: 0.14rem;
  }
}
.banner {
  height: 0;
  overflow: hidden;
  padding-bottom: 25.4%;
  &__img {
    width: 100%;
  }
}
.icons {
  display: flex;
  flex-wrap: wrap;
  margin-top: 0.16rem;
  &__item {
    width: 20%;
    &__img {
      display: block;
      width: 0.4rem;
      height: 0.4rem;
      margin: 0 auto;
    }
    &__desc {
      margin: 0.06rem 0 0.16rem 0;
      text-align: center;
      color: $content-fontcolor;
    }
  }
}
.gap {
  margin: 0 -0.18rem;
  height: 0.1rem;
  background: $content-bgColor;
}
</style>
