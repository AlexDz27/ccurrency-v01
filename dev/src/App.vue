<template>
  <h2>Base currency: USD</h2>
  <input v-model="usd" @keypress="allowOnlyNumeric" @keyup="convert" class="input">

  <h3>BYN</h3>
  <input v-model="byn" class="input">
</template>

<script>
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

      const BYN_RATIO = 2.5374;

      // TODO: redo the algorithm
      this.byn = Math.round((this.usd * BYN_RATIO + Number.EPSILON) * 100) / 100;
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

.input {
  width: 100%;
  box-sizing: border-box;
  font-size: 32px;
}
</style>