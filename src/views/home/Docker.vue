<template>
  <div class="docker">
    <div
      v-for="(item, index) in dockerList"
      :key="item.icon"
      :class="{ docker__item: true, 'docker__item--active': index === 0 }"
    >
      <router-link :to="item.to">
        <div class="iconfont" v-html="item.icon"></div>
        <div class="docker__title">{{ item.text }}</div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Docker',

  setup () {
    const dockerList = [
      {
        icon: '&#xe6f3;',
        text: '首页',
        to: { name: 'Home' }
      },
      {
        icon: '&#xe638;',
        text: '购物车',
        to: { name: 'CartList' }
      },
      {
        icon: '&#xe61e;',
        text: '订单',
        to: { name: 'OrderConfirmation' }
      },
      {
        icon: '&#xe660;',
        text: '我的',
        to: { name: 'Home' }
      }
    ]
    return {
      dockerList
    }
  },
  watch: {},

  computed: {},

  mounted () {},

  methods: {}
}
</script>

<style lang="scss" scoped>
@import '../../style/variables.scss';
@import '../../style/mixins.scss';

.docker {
  display: flex;
  box-sizing: border-box;
  position: absolute;
  padding: 0 0.18rem;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 0.49rem;
  border-top: 0.01rem solid $content-bgColor;
  color: $content-fontcolor;
  &__item {
    flex: 1;
    text-align: center;
    .iconfont {
      margin: 0.07rem 0 0.02rem 0;
      font-size: 0.18rem;
    }
    a {
      color: $content-fontcolor;
      text-decoration: none;
    }
    &--active {
      a {
        color: #1fa4fc;
      }
    }
  }
  &__title {
    font-size: 0.2rem;
    transform: scale(0.5, 0.5);
    transform-origin: center top;
  }
}
</style>
