<template>
  <div class="content">
    <div class="product">
      <div v-for="(product, i) in productList" :key="i" class="product__card">
        <div class="product__image">
          <img :src="require(`@/assets${product.image}`)" :alt="product.name" />
        </div>
        <div class="product__info">
          <span class="product__name">
            {{ product.name }}
          </span>
          <div class="product__price">
            <p class="spot-price">{{ product.bestPriceFormated }}</p>
            <p class="split-price">
              10x de R$ {{ splitPrice(product.bestPrice) }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      productList: null,
    }
  },
  created() {
    this.getProductList()
  },
  methods: {
    getProductList() {
      this.$http
        .get('/products.json')
        .then(res => (this.productList = res.data.cart.item))
    },
    splitPrice(price) {
      return (price / Math.pow(10, 3))
        .toFixed(2)
        .toString()
        .replace('.', ',')
    },
  },
}
</script>

<style scoped>
.content {
  padding: 30px;
  max-width: 1440px;
  margin: 0 auto;
}

.product__card {
  margin: 15px;
  width: 250px;
  height: 350px;
  border-radius: 15px;
  box-shadow: 0 4px 6px #dddddd;
  transition: all 0.3s;
}

.product__card:hover {
  box-shadow: 0 4px 10px #cccccc;
  transform: translateY(-1px);
}

.product__image {
  height: 50%;
  text-align: center;
  padding: 5px;
}

.product__info {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 10px;
  height: 50%;
}

.product__name {
  font-size: 12px;
}

.product__price {
  padding: 5px;
  background-color: #00bc0e;
  color: white;
  border-radius: 8px;
}

.spot-price {
  font-weight: 600;
  padding-bottom: 5px;
}

.split-price {
  font-size: 10px;
}

.product {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
