<template>
  <p class="input-container">
    <span class="input-currency">USD:</span> <input v-model="usd" @keypress="allowOnlyNumeric" @keyup="convert" class="input">
  </p>

  <p class="input-container">
    <span class="input-currency">BYN:</span> <input v-model="byn" @keypress="allowOnlyNumeric" @keyup="convert" class="input">
  </p>
</template>

<script>
import { BYN_RATIO } from '@/ratios';

export default {
  name: 'App',
  data() {
    return {
      usd: 1,
      byn: 0
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
      if (this.usd === '') {
        this.byn = '';
        return;
      }

      this.byn = Number((this.usd * BYN_RATIO).toFixed(4));
    }
  },
  mounted() {
    this.convert();
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