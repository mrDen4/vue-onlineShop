<template>
  <main class="content container" v-if="productLoading"><h1>Идет загрузка продукта ...</h1></main>
  <main class="content container" v-else-if="productInfo">
    <div class="content__top">
      <ul class="breadcrumbs">
        <li class="breadcrumbs__item">
          <router-link class="breadcrumbs__link" :to="{name: 'main'}">
            Каталог
          </router-link>
        </li>
        <li class="breadcrumbs__item">
          <router-link class="breadcrumbs__link" :to="{name: 'main'}">
            {{category.title}}
          </router-link>
        </li>
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link">
            {{product.title}}
          </a>
        </li>
      </ul>
    </div>

    <section class="item">
      <div class="item__pics pics">
        <div class="pics__wrapper">
          <img width="570" height="570"
               :src="product.image.file.url"
               :alt="product.title">
        </div>
      </div>

      <div class="item__info">
        <span class="item__code">Артикул: {{product.id}}</span>
        <h2 class="item__title">
          {{product.title}}
        </h2>
        <div class="item__form">
          <form class="form" action="#" method="POST" @submit.prevent="addToCart">
            <b class="item__price">
              {{pricePretty}} ₽
            </b>

            <fieldset class="form__block">
              <legend class="form__legend">Цвет:</legend>
              <ul class="colors">
                <li class="colors__item">
                  <label class="colors__label" for="blue">
                    <input class="colors__radio sr-only" type="radio" name="color-item"
                           value="blue" checked="" id="blue">
                    <span class="colors__value" style="background-color: #73B6EA;">
                    </span>
                  </label>
                </li>
                <li class="colors__item">
                  <label class="colors__label" for="yellow">
                    <input class="colors__radio sr-only" type="radio" name="color-item"
                           value="yellow" id="yellow">
                    <span class="colors__value" style="background-color: #FFBE15;">
                    </span>
                  </label>
                </li>
                <li class="colors__item">
                  <label class="colors__label" for="gray">
                    <input class="colors__radio sr-only" type="radio" name="color-item"
                           value="gray" id="gray">
                    <span class="colors__value" style="background-color: #939393;">
                  </span></label>
                </li>
              </ul>
            </fieldset>

            <fieldset class="form__block">
              <legend class="form__legend">Объемб в ГБ:</legend>

              <ul class="sizes sizes--primery">
                <li class="sizes__item">
                  <label class="sizes__label" for="32gb">
                    <input class="sizes__radio sr-only" type="radio" name="sizes-item"
                           value="32" id="32gb">
                    <span class="sizes__value">
                      32gb
                    </span>
                  </label>
                </li>
                <li class="sizes__item">
                  <label class="sizes__label" for="64gb">
                    <input class="sizes__radio sr-only" type="radio" name="sizes-item"
                           value="64" id="64gb">
                    <span class="sizes__value">
                      64gb
                    </span>
                  </label>
                </li>
                <li class="sizes__item">
                  <label class="sizes__label" for="128gb">
                    <input class="sizes__radio sr-only"
                           type="radio" name="sizes-item" value="128" checked="" id="128gb">
                    <span class="sizes__value">
                      128gb
                    </span>
                  </label>
                </li>
              </ul>
            </fieldset>

            <div class="item__row">
              <div class="form__counter">
                <button type="button" aria-label="Убрать один товар"
                        @click="() => this.count != 0 ? this.count -= 1 : this.count">
                  <svg width="12" height="12" fill="currentColor">
                    <use xlink:href="#icon-minus"></use>
                  </svg>
                </button>

                <input aria-label="test" type="text" v-model="count" name="count">

                <button type="button" aria-label="Добавить один товар"
                        @click="() => this.count += 1">
                  <svg width="12" height="12" fill="currentColor">
                    <use xlink:href="#icon-plus"></use>
                  </svg>
                </button>
              </div>

              <button class="button button--primery" type="submit"
                      :disabled="loadingProductAddToCart">
                В корзину
              </button>
              <div v-show="loadingProductAddToCart">Товар добавляется в корзину</div>
              <div v-show="productAddToCart">Товар успешно добавлен в корзину</div>
            </div>
          </form>
        </div>
      </div>

      <div class="item__desc">
        <ul class="tabs">
          <li class="tabs__item">
            <a class="tabs__link tabs__link--current">
              Описание
            </a>
          </li>
          <li class="tabs__item">
            <a class="tabs__link" href="#">
              Характеристики
            </a>
          </li>
          <li class="tabs__item">
            <a class="tabs__link" href="#">
              Гарантия
            </a>
          </li>
          <li class="tabs__item">
            <a class="tabs__link" href="#">
              Оплата и доставка
            </a>
          </li>
        </ul>

        <div class="item__content">
          <p>
            Навигация GPS, ГЛОНАСС, BEIDOU Galileo и QZSS<br>
            Синхронизация со смартфоном<br>
            Связь по Bluetooth Smart, ANT+ и Wi-Fi<br>
            Поддержка сторонних приложений<br>
          </p>

          <a href="#">
            Все характеристики
          </a>

          <h3>Что это?</h3>

          <p>
          </p>
          <p> Wahoo ELEMNT BOLT GPS – это велокомпьютер, который позволяет оптимизировать свои
            велотренировки, сделав их максимально эффективными. Wahoo ELEMNT BOLT GPS
            синхронизируется с датчиками поANT, объединяя полученную с них информацию. Данные
            отображаются на дисплее, а также сохраняются на смартфоне. При этом на мобильное
            устройство можно установить как фирменное приложение, так и различные приложения
            сторонних разработчиков. Велокомпьютер точно отслеживает местоположение, принимая сигнал
            с целого комплекса спутников. Эта информация позволяет смотреть уже преодоленные
            маршруты ипланировать новые велопрогулки.
          </p>

          <h3>Дизайн</h3>

          <p>
            Велокомпьютер Wahoo ELEMNT BOLT очень компактный. Размеры устройства составляют всего
            74,6 x 47,3 x 22,1 мм. что не превышает габариты смартфона. Корпус гаджета выполнен из
            черного пластика. Наобращенной к пользователю стороне расположен дисплей диагональю 56
            мм. На дисплей выводятся координаты и скорость, а также полученная со смартфона и
            синхронизированных датчиков информация: интенсивность, скорость вращения педалей, пульс
            и т.д. (датчики не входят в комплект поставки). Корпус велокомпьютера имеет степень
            защиты от влаги IPX7. Это означает, что устройство не боится пыли, а также выдерживает
            кратковременное (до 30 минут) погружение в воду на глубину не более 1 метра.
          </p>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import goToPage from '@/helpers/goToPage';
import axios from 'axios';
import { BASE_URL_API } from '@/confing';
import { mapActions } from 'vuex';
import numberFormat from '@/helpers/numberFormat';

export default {
  props: {
    productId: { type: [Number, String], required: true },
  },
  data() {
    return {
      count: 1,
      productInfo: null,
      productLoading: true,
      productAddToCart: false,
      loadingProductAddToCart: false,
    };
  },
  computed: {
    product() {
      return this.productInfo;
    },
    category() {
      return this.productInfo.category;
    },
    pricePretty() {
      return numberFormat(this.product.price);
    },
  },
  methods: {
    ...mapActions(['addToCartProducts']),
    loadProduct() {
      axios.get(`${BASE_URL_API}/products/${+this.productId}`)
        .then((response) => { this.productInfo = response.data; })
        .then(() => { this.productLoading = false; });
    },
    goToPage,
    addToCart() {
      this.productAddToCart = false;
      this.loadingProductAddToCart = true;
      this.addToCartProducts({ productId: this.product.id, amount: this.count })
        .then(() => {
          this.productAddToCart = true;
          this.loadingProductAddToCart = false;
        });
    },
  },
  created() {
    this.loadProduct();
  },
  beforeRouteUpdate() {
    this.loadProduct();
  },
};

</script>
