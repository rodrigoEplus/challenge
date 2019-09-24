<template>
  <div class="shopping-cart-wrapper">
    <div class="shopping-cart__icon" @click="openShoppingCart">
      <img src="@/assets/icons/shopping_cart.svg" alt="User menu" />
    </div>
    <div
      :class="{
        'shopping-cart': true,
        'shopping-cart--show': showShoppingCart,
      }"
    >
      <div class="shopping-cart__products">
        <div
          v-for="(item, i) in cartItems"
          :key="i"
          class="shopping-cart__products__item"
        >
          <img
            :src="require(`@/assets${item.image}`)"
            alt=""
            class="shopping-cart__products__item__image"
          />
          <span class="shopping-cart__products__item__name">
            {{ item.name }}
          </span>
          <span class="shopping-cart__products__item__quantity">
            Qtd. {{ item.quantity }}
          </span>
          <span class="shopping-cart__products__item__price">
            {{ item.bestPriceFormated }}
          </span>
        </div>
      </div>
      <div class="shopping-cart__total-price">
        <span>
          Total do pedido:
          <span class="shopping-cart__total-price--bold">
            R$ {{ totalPrice }}
          </span>
        </span>
      </div>
      <div class="shopping-cart__button">
        <span>finalizar compra</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ShoppingCart',
  data() {
    return {
      cartItems: [],
      showShoppingCart: false,
    }
  },
  computed: {
    totalPrice() {
      return this.moveDecimalCommaToLeft(
        this.calculateTotalPrice(this.cartItems)
      )
    },
  },
  created() {
    this.getProductList()
  },
  methods: {
    getProductList() {
      this.$http
        .get('/products.json')
        .then(res => (this.cartItems = res.data.cart.item))
    },
    calculateTotalPrice(shoppingCart) {
      if (!shoppingCart) return '0,00'
      return shoppingCart
        .map(item => item.bestPrice)
        .reduce((oldPrice, newPrice) => oldPrice + newPrice, 0)
    },
    moveDecimalCommaToLeft(value) {
      return (value / Math.pow(10, 2))
        .toFixed(2)
        .toString()
        .replace('.', ',')
    },
    openShoppingCart() {
      return (this.showShoppingCart = !this.showShoppingCart)
    },
  },
}
</script>

<style scoped>
.shopping-cart-wrapper {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  height: 100%;
  width: 100%;
}

.shopping-cart {
  width: 250px;
  z-index: 8;
  position: absolute;
  display: none;
  right: 0;
  top: 100%;
  box-shadow: 0 4px 5px #ccc;
}

.shopping-cart-wrapper:hover .shopping-cart {
  display: block;
}

.shopping-cart--show {
  display: block;
}

.shopping-cart:after {
  bottom: 100%;
  left: 82%;
  border: solid transparent;
  content: ' ';
  height: 0;
  width: 0;
  position: absolute;
  pointer-events: none;
  border-bottom-color: #eee;
  border-width: 10px;
}

.shopping-cart__products {
  height: 180px;
  overflow: auto;
  padding: 5px;
  background-color: #eee;
}

.shopping-cart__products__item {
  width: 100%;
  padding: 5px;
  border-bottom: 1px solid #ddd;
  display: grid;
  grid-template-columns: auto auto auto;
  grid-template-rows: 1fr 1fr;
  grid-template-areas:
    'image name name'
    'image quantity price';
}

.shopping-cart__products__item__image {
  height: 50px;
  grid-area: image;
}

.shopping-cart__products__item__name {
  font-size: 12px;
  grid-area: name;
  padding: 0 5px;
  width: 100%;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-overflow: ellipsis;
}

.shopping-cart__products__item__quantity {
  grid-area: quantity;
  padding: 5px;
  font-size: 12px;
}

.shopping-cart__products__item__price {
  grid-area: price;
  padding: 5px;
  font-size: 14px;
  font-weight: 600;
  color: #00bc0e;
}

.shopping-cart__total-price {
  height: 50px;
  background-color: #ddd;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 14px;
}

.shopping-cart__total-price--bold {
  font-weight: 600;
}

.shopping-cart__button {
  height: 50px;
  background-color: #00bc0e;
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
  font-weight: 600;
  cursor: pointer;
}
</style>
