<template>
  <div class="shop">
    <img class="shop__img" :src="item.imgUrl" alt="" />
    <div
      :class="{
        shop__content: true,
        'shop__content--bordered': hideBorder ? false : true
      }"
    >
      <div class="shop__content__title">{{ item.name }}</div>
      <div class="shop__content__tags">
        <span class="shop__content__tag">月售： {{ item.sales }}</span>
        <span class="shop__content__tag">起送：{{ item.expressLimit }}</span>
        <span class="shop__content__tag"
          >基础运费: {{ item.expressPrice }}</span
        >
      </div>
      <p class="shop__content__highlight">{{ item.slogan }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ShopInfo',

  props: {
    item: {
      type: Object
    },
    hideBorder: {
      type: Boolean
    }
  },

  components: {},

  setup () {
    return {}
  }
}
</script>

<style lang="scss" scoped>
@import '../style/variables.scss';

.shop {
  display: flex;
  padding-top: 0.12rem;
  &__img {
    width: 0.56rem;
    height: 0.56rem;
    margin-right: 0.16rem;
  }
  &__content {
    flex: 1;
    padding-bottom: 0.12rem;
    &--bordered {
      border-bottom: 1px solid $content-bgColor;
    }
    &__title {
      line-height: 0.22rem;
      font-size: 0.16rem;
      color: $content-fontcolor;
    }
    &__tags {
      margin-top: 0.08rem;
      line-height: 0.18rem;
      font-size: 0.13rem;
      color: $content-fontcolor;
    }
    &__tag {
      margin-right: 0.16rem;
    }
    &__highlight {
      margin: 0.08rem 0 0 0;
      color: $highlight-fontColor;
      line-height: 0.18rem;
      font-size: 0.13rem;
    }
  }
}
</style>
