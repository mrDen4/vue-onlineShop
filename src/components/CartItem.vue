<template>
  <li class="cart__item product">
    <div class="product__pic">
      <img :src="item.product.image" width="120" height="120"
           :alt="item.product.title">
    </div>
    <h3 class="product__title">
      {{item.product.title}}
    </h3>
    <span class="product__code">
                  Артикул: {{item.product.id}}
                </span>

    <div class="product__counter form__counter">
      <button type="button" aria-label="Убрать один товар" @click="() => this.amount -= 1">
        <svg width="10" height="10" fill="currentColor">
          <use xlink:href="#icon-minus"></use>
        </svg>
      </button>

      <input aria-label="count" type="text" v-model.number="amount" name="count">

      <button type="button" aria-label="Добавить один товар" @click="() => this.amount += 1">
        <svg width="10" height="10" fill="currentColor">
          <use xlink:href="#icon-plus"></use>
        </svg>
      </button>
    </div>

    <b class="product__price">
      {{totalPricePretty}} ₽
    </b>

    <button class="product__del button-del"
            type="button" aria-label="Удалить товар из корзины"
            @click="deleteProduct(item.product.id)">
      <svg width="20" height="20" fill="currentColor">
        <use xlink:href="#icon-close"></use>
      </svg>
    </button>
  </li>
</template>

<script>
import numberFormat from '@/helpers/numberFormat';
import { mapActions } from 'vuex';

export default {
  props: ['item'],
  computed: {
    totalPricePretty() {
      return numberFormat(this.item.amount * this.item.product.price);
    },
    amount: {
      get() {
        return this.item.amount;
      },
      set(value) {
        this.$store.dispatch('updateCartProductsAmount', { productId: this.item.productId, amount: value });
      },
    },
  },
  methods: {
    ...mapActions({ deleteProduct: 'deleteCartProduct' }),
  },
};
</script>
