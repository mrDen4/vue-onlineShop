<template>
  <div class="cart__block">
    <ul class="cart__orders">
      <li class="cart__order" v-for="product in products" :key="product.id">
        <h3>{{product.product.title}}</h3>
        <b>{{totalPricePretty}} ₽</b>
        <span>Артикул: {{ product.product.id }}</span>
      </li>
    </ul>

    <div class="cart__total">
      <p>Доставка: <b>500 ₽</b></p>
      <p>Итого: <b>3</b> товара на сумму <b>{{sumProductsPrice + 500}} ₽</b></p>
    </div>

    <button class="cart__button button button--primery" type="submit">
      Оформить заказ
    </button>
  </div>
</template>

<script>
import numberFormat from '@/helpers/numberFormat';
import { mapGetters } from 'vuex';

export default {
  computed: {
    totalPricePretty() {
      return numberFormat(this.item.amount * this.item.product.price);
    },
    ...mapGetters({ products: 'cartDetailProducts', sumProductsPrice: 'sumCartProducts' }),
  },
};
</script>
