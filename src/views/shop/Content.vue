<template>
  <div class="content">
    <div class="category">
      <div
        v-for="item in categories"
        :key="item.tab"
        :class="{
          category__item: true,
          'category__item--active': currentTab === item.tab
        }"
        @click="() => handleTabClick(item.tab)"
      >
        {{ item.name }}
      </div>
      <!-- <div class="category__item">休闲食品</div>
      <div class="category__item">时令蔬菜</div>
      <div class="category__item">肉蛋家禽</div> -->
    </div>
    <div class="product">
      <div class="product__item" v-for="item in list" :key="item._id">
        <img class="product__item__img" :src="item.imgUrl" alt="" />
        <div class="product__item__detail">
          <h4 class="product__item__title">{{ item.name }}</h4>
          <p class="product__item__sales">月售{{ item.sales }}件</p>
          <p class="product__item__price">
            <span class="product__item__yen">&yen;</span>{{ item.price }}
            <span class="product__item__origin">{{ item.oldPrice }}</span>
          </p>
        </div>
        <div class="product__number">
          <span
            class="product__number__minus"
            @click="
              () => {
                changeCartItem(shopId, item._id, item, -1, shopName)
              }
            "
            >-</span
          >
          {{ getProductCartCount(shopId, item._id) }}
          <span
            class="product__number__plus"
            @click="
              () => {
                changeCartItem(shopId, item._id, item, 1, shopName)
              }
            "
            >+</span
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, ref, toRefs, watchEffect } from 'vue'
import { useRoute } from 'vue-router'
import { useStore } from 'vuex'
import { get } from '../../utils/request'
import { useCommonCartEffect } from '../../effects/cartEffects'

const categories = [
  {
    name: '全部商品',
    tab: 'all'
  },
  {
    name: '秒杀',
    tab: 'seckill'
  },
  {
    name: '新鲜水果',
    tab: 'fruit'
  }
]

const useTabEffect = () => {
  const currentTab = ref(categories[0].tab)

  const handleTabClick = tab => {
    currentTab.value = tab
  }

  return {
    currentTab,
    handleTabClick
  }
}

const useCurrentListEffect = (currentTab, shopId) => {
  const content = reactive({
    list: []
  })

  const getContentData = async () => {
    const result = await get(`/api/shop/${shopId}/products`, {
      tab: currentTab.value
    })
    if (result?.errno === 0 && result?.data) {
      content.list = result.data
    }
  }

  watchEffect(() => {
    getContentData()
  })

  const { list } = toRefs(content)

  return {
    list
  }
}

const userCartEffect = () => {
  const store = useStore()

  const { changeCartItemInfo, cartList } = useCommonCartEffect()

  const changeShopName = (shopId, shopName) => {
    store.commit('changeShopName', { shopId, shopName })
  }

  const changeCartItem = (shopId, productId, item, num, shopName) => {
    changeCartItemInfo(shopId, productId, item, num)
    changeShopName(shopId, shopName)
  }

  const getProductCartCount = (shopId, productId) => {
    return cartList?.[shopId]?.productList?.[productId]?.count || 0
  }

  return { cartList, changeCartItem, getProductCartCount }
}

export default {
  name: 'Content',

  props: ['shopName'],

  setup () {
    const route = useRoute()

    const shopId = route.params.id

    const { currentTab, handleTabClick } = useTabEffect()

    const { list } = useCurrentListEffect(currentTab, shopId)

    const { cartList, changeCartItem, getProductCartCount } = userCartEffect()

    return {
      currentTab,
      categories,
      handleTabClick,
      list,
      changeCartItem,
      getProductCartCount,
      cartList,
      shopId
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../../style/variables.scss';
@import '../../style/mixins.scss';

.content {
  display: flex;
  position: absolute;
  left: 0;
  right: 0;
  top: 1.5rem;
  bottom: 0.5rem;
}
.category {
  overflow-y: scroll;
  height: 100%;
  width: 0.76rem;
  background: $search-bgColor;
  &__item {
    line-height: 0.4rem;
    text-align: center;
    font-size: 0.14rem;
    color: $content-fontcolor;
    &--active {
      background: $bgColor;
    }
  }
}
.product {
  overflow-y: scroll;
  flex: 1;
  &__item {
    position: relative;
    display: flex;
    padding: 0.12rem 0;
    margin: 0 0.16rem;
    border-bottom: 0.01rem solid $content-bgColor;
    &__detail {
      overflow: hidden;
    }
    &__img {
      width: 0.68rem;
      height: 0.68rem;
      margin-right: 0.16rem;
    }
    &__title {
      margin: 0;
      line-height: 0.2rem;
      font-size: 0.14rem;
      color: $content-fontcolor;
      @include ellipsis;
    }
    &__sales {
      margin: 0.06rem 0;
      line-height: 0.16rem;
      font-size: 0.12rem;
      color: $content-fontcolor;
    }
    &__price {
      margin: 0;
      line-height: 0.2rem;
      font-size: 0.14rem;
      color: $highlight-fontColor;
    }
    &__yen {
      font-size: 0.12rem;
    }
    &__origin {
      margin-left: 0.06rem;
      line-height: 0.2rem;
      font-size: 0.12rem;
      color: $light-fontColor;
      text-decoration: line-through;
    }
  }
  &__number {
    position: absolute;
    right: 0;
    bottom: 0.12rem;
    &__minus,
    &__plus {
      display: inline-block;
      width: 0.2rem;
      height: 0.2rem;
      line-height: 0.16rem;
      font-size: 0.2rem;
      border-radius: 50%;
      text-align: center;
    }
    &__minus {
      margin-right: 0.05rem;
      border: 0.01rem solid $medium-fontColor;
      color: $medium-fontColor;
    }
    &__plus {
      margin-left: 0.05rem;
      background: $btn-bgColor;
      color: $bgColor;
    }
  }
}
</style>
