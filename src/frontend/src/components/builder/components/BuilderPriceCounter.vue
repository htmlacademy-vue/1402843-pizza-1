<template>
  <p>Итого: {{ countPrice() }} ₽</p>
</template>

<script>
  export default {
    name: 'BuilderPriceCounter',
    props: {
      priceData: {
        type: Object,
        required: true,
      },
    },
    methods: {
      countPrice() {
        // мультипликатор размера х (стоимость теста + соус + ингредиенты)
        let pizzaPrice = 0;
        if (this.priceData.doughPrice || this.priceData.saucePrice || this.priceData.ingredientPrice) {
          pizzaPrice = this.priceData.doughPrice + this.priceData.saucePrice + this.priceData.ingredientPrice;
        }
        if (this.priceData.sizeMultiplier) {
          pizzaPrice = pizzaPrice * this.priceData.sizeMultiplier;
        }
        return pizzaPrice;
      },
    },
  };

</script>

<style scoped>

</style>
