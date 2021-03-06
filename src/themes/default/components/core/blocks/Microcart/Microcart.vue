<template>
  <div
    class="microcart mw-100 fixed c-darkgray"
    :class="[items.length ? 'bg-lightgray' : 'bg-white', { active: isOpen }]"
  >
    <div class="row middle-xs bg-white top-sm">
      <div class="col-xs-10">
        <h2
          v-if="items.length"
          class="c-darkgray mt60 mb35 ml40 heading"
        >
          {{ $t('Shopping cart') }}
        </h2>
      </div>
      <div class="col-xs-2 end-xs">
        <button type="button" class="p0 brdr-none bg-transparent">
          <i class="material-icons p15 close c-darkgray" @click="closeMicrocart">
            close
          </i>
        </button>
      </div>
    </div>

    <h4 v-if="!items.length" class="c-darkgray ml30">
      {{ $t('Your shopping cart is empty.') }}
    </h4>
    <div v-if="!items.length" class="ml30" @click="closeMicrocart">
      {{ $t("Don't hesitate and") }}
      <router-link to="/">
        {{ $t('browse our catalog') }}
      </router-link>
      {{ $t('to find something beautiful for You!') }}
    </div>
    <ul v-if="items.length" class="bg-white m0 px40 pb40 products">
      <product v-for="product in items" :key="product.sku" :product="product" />
    </ul>
    <div v-if="items.length" class="summary px40 c-darkgray serif">
      <h3 class="m0 pt40 mb30 weight-400 summary-heading">
        {{ $t('Shopping summary') }}
      </h3>
      <div class="row py20">
        <div class="col-xs">
          {{ $t('Subtotal inc. tax') }}
        </div>
        <div class="col-xs align-right">
          {{ subtotalInclTax | price }}
        </div>
      </div>
      <div class="row py20">
        <div class="col-xs">
          {{ $t('Shipping') }} ({{ shipping.name }})
        </div>
        <div class="col-xs align-right">
          {{ shipping.costInclTax | price }}
        </div>
      </div>
      <div class="row py20">
        <div class="col-xs">
          {{ $t('Payment') }} ({{ payment.name }})
        </div>
        <div class="col-xs align-right" v-if="payment.cost > 0">
          {{ payment.costInclTax | price }}
        </div>
      </div>
      <div class="row pt30 pb20 weight-700 middle-xs">
        <div class="col-xs h4 total-price-label">
          {{ $t('Total inc. tax') }}
        </div>
        <div class="col-xs align-right h2 total-price-value">
          {{ totalInclTax | price }}
        </div>
      </div>
    </div>
    <div
      class="row py20 px40 middle-xs actions"
      v-if="items.length && !isCheckoutMode"
    >
      <div class="col-xs-12 col-sm first-sm">
        <router-link to="/" class="no-underline c-gray-secondary link">
          <span @click="closeMicrocart">
            {{ $t('Return to shopping') }}
          </span>
        </router-link>
      </div>
      <div class="col-xs-12 first-xs col-sm end-sm">
        <router-link
          class="no-underline inline-flex h4 checkout-button bg-darkgray link checkout"
          :to="{ name: 'checkout' }"
        >
          <span
            class="c-white py20 px70"
            @click="closeMicrocart"
          >
            {{ $t('Go to checkout') }}
          </span>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { coreComponent } from 'lib/themes'
import Product from './Product'

export default {
  components: {
    Product
  },
  mixins: [coreComponent('core/blocks/Microcart/Microcart')]
}
</script>

<style lang="scss" scoped>
  @import "~theme/css/animations/transitions";

  .microcart {
    top: 0;
    right: 0;
    z-index: 3;
    height: 100%;
    width: 800px;
    min-width: 320px;
    transform: translateX(100%);
    transition: transform 300ms $motion-main;
    overflow-y: auto;
    overflow-x: hidden;
    &.active {
      transform: translateX(0)
    }
  }

  .heading {
    @media (max-width: 767px) {
      margin: 12px 0 12px 15px;
      font-size: 24px;
    }

    i {
      opacity: 0.6;
      &:hover,
      &:focus {
        opacity: 1;
      }
    }
  }

  .products {
    @media (max-width: 767px) {
      padding: 30px 15px;
    }
  }

  .actions {
    @media (max-width: 767px) {
      padding: 0 15px;
    }
    .link {
      @media (max-width: 767px) {
        display: flex;
        justify-content: center;
        padding: 20px 70px;
        &.checkout {
          margin-top: 55px;
          padding: 0;
        }
      }
    }
  }

  .summary {
    @media (max-width: 767px) {
      padding:  0 15px;
      font-size: 12px;
    }
  }

  .summary-heading {
    @media (max-width: 767px) {
      font-size: 18px;
    }
  }

  .total-price-label {
    @media (max-width: 767px) {
      font-size: 18px;
    }
  }

  .total-price-value {
    @media (max-width: 767px) {
      font-size: 24px;
    }
  }
</style>
