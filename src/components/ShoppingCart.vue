<template>
  <div class="shopping-cart-wrapper">
    <div class="shopping-cart__icon" @click="toggleShoppingCart">
      <img src="@/assets/icons/shopping_cart.svg" alt="User menu" />
      <span v-if="cartItems.length" class="shopping-cart__badge">
        {{ cartItems.length || '' }}
      </span>
    </div>
    <div
      v-if="cartItems.length"
      :class="{
        'shopping-cart': true,
        'shopping-cart--show': shoppingCart,
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
    shoppingCart() {
      console.log(this.showShoppingCart)
      return this.showShoppingCart
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
        .map(item => item.bestPrice * item.quantity)
        .reduce((oldPrice, newPrice) => oldPrice + newPrice, 0)
    },
    moveDecimalCommaToLeft(value, slots = 2, precision = 2) {
      return (value / Math.pow(10, slots))
        .toFixed(precision)
        .toString()
        .replace('.', ',')
    },
    toggleShoppingCart() {
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
  height: 100%;
  width: 100%;
}

.shopping-cart {
  width: 300px;
  z-index: 8;
  position: absolute;
  display: none;
  right: 0;
  top: 100%;
  box-shadow: 0 5px 5px rgba(0, 0, 0, 0.2);
}

.shopping-cart__badge {
  position: absolute;
  bottom: 10px;
  right: 3px;
  background-color: #00bc0e;
  border-radius: 10px;
  color: white;
  display: inline-block;
  font-size: 8px;
  padding: 2px 7px;
}

.shopping-cart--show {
  display: block;
}

.shopping-cart:after {
  bottom: 100%;
  right: 10px;
  border: solid transparent;
  content: ' ';
  height: 0;
  width: 0;
  position: absolute;
  border-bottom-color: #eee;
  border-width: 10px;
}

.shopping-cart__products {
  max-height: 250px;
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

@keyframes unfold {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@media only screen and (min-width: 1024px) {
  .shopping-cart__badge {
    bottom: 20px;
    right: 10px;
    font-size: 10px;
  }

  .shopping-cart-wrapper:hover > .shopping-cart {
    transform-origin: top right;
    display: block;
    perspective: 100px;
    animation: unfold 0.3s ease-in-out;
  }

  .shopping-cart:after {
    right: 25px;
  }
}
</style>
