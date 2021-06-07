<template>
  <p class="input-container">
    <span class="input-currency">{{ currency.name }}:</span>
    <input @focus="makeActive" v-model="currency.amount" @keypress="allowOnlyNumeric" @keyup="convert" class="input">
  </p>
</template>

<script>
export default {
  props: {
    currency: Object,
    allowOnlyNumeric: Function,
    convert: Function,
  },
  methods: {
    makeActive() {
      this.$emit('makeActive', this.currency.id);
    }
  }
}
</script>