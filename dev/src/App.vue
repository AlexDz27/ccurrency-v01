<template>
  <Input
    @click="log"
    v-for="currency in currencies"
    :currency="currency"
    :key="currency.id"
    :allowOnlyNumeric="allowOnlyNumeric"
    :convert="convert"
    @makeActive="makeActive"
  />
</template>

<script>
import Input from '@/Input';

import * as ratio from '@/ratios';

export default {
  components: { Input },
  data() {
    return {
      currencies: {
        usd: {
          id: 'usd',
          name: 'USD',
          amount: 1
        },
        byn: {
          id: 'byn',
          name: 'BYN',
          amount: 0
        },
        eur: {
          id: 'eur',
          name: 'EUR',
          amount: 0
        },
        rub: {
          id: 'rub',
          name: 'RUB',
          amount: 0
        }
      },

      activeCurrId: 'usd'
    }
  },
  methods: {
    allowOnlyNumeric(evt) {
      /**
       * Only digits and dot "." are allowed
       * @const
       * @type {RegExp}
       */
      const REGEX = /^[\d.]*$/;

      if (!REGEX.test(evt.key)) evt.preventDefault();
    },

    convert() {
      const currencies = Object.keys(this.currencies).filter(curr => curr.id !== 'usd');
      for (const currency of currencies) {
        if (this.activeCurrId !== 'usd') {
          this.currencies.usd.amount = Number((this.currencies[this.activeCurrId].amount / ratio[this.activeCurrId]).toFixed(4));
        }

        if (currency.id === this.activeCurrId) continue;

        this.currencies[currency.id].amount = Number((this.currencies.usd.amount * ratio[currency.id]).toFixed(4));
      }
    },

    makeActive(currencyId) {
      this.activeCurrId = currencyId;
    },

    log() {
      console.log(this.activeCurrId)
    }
  },
  mounted() {
    // TODO: refactor - need method for converting
    const currencies = Object.keys(this.currencies).filter(curr => curr.id !== 'usd');
    for (const currency of currencies) {
      if (currency.id === this.activeCurrId) continue;

      this.currencies[currency.id].amount = Number((this.currencies.usd.amount * ratio[currency.id]).toFixed(4));
    }
  }
}
</script>

<style>
body {
  width: 315px;
  margin-left: auto;
  margin-right: auto;

  background-color: rgba(0, 0, 0, .3); /* TODO: remove when deploying */
}

#app {
  font-family: Arial, 'sans-serif';
  border-top: 1px solid transparent;
  width: 300px;
  height: 400px;
  padding: 0 15px;
  box-sizing: border-box;
  margin: 0 auto;
  text-align: center;

  background-color: #fff; /* TODO: remove when deploying */
}

.input-container {
  display: flex;
  align-items: center;
  font-size: 32px;
}

.input-currency {
  margin-right: 9px;
}

.input {
  width: 100%;
  box-sizing: border-box;
  font-size: 32px;
}
</style>