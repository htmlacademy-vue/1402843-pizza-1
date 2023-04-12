<template>
  <div>
    <form action="#" method="post">
      <div class="content__wrapper">
        <h1 class="title title--big">Конструктор пиццы</h1>

        <BuilderDoughtSelector @doughSelected="pizzaData.dough=$event"></BuilderDoughtSelector>
        <BuilderSizeSelector @sizeSelected="pizzaData.size=$event"></BuilderSizeSelector>
        <BuilderIngredientsSelector
          @sauceSelected="pizzaData.sauce=$event"
          @fillingSelected="pizzaData.filling[$event.value]=$event"
        >
        </BuilderIngredientsSelector>

        <div class="content__pizza">
          <BuilderPizzaView
            @onInput="pizzaData.name=$event"
            :pizzaConsist="pizzaData"
          >
          </BuilderPizzaView>

          <div class="content__result">
            <BuilderPriceCounter :priceData="pizzaPriceData"></BuilderPriceCounter>
            <Button
              :class="{'button--disabled': !isReadyToCook}"
              :disabled="!isReadyToCook"
            >
            </Button>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
  import BuilderDoughtSelector from '@/components/builder/components/BuilderDoughtSelector.vue';
  import BuilderSizeSelector from '@/components/builder/components/BuilderSizeSelector.vue';
  import BuilderIngredientsSelector from '@/components/builder/components/BuilderIngredientsSelector.vue';
  import BuilderPizzaView from '@/components/builder/components/BuilderPizzaView.vue';
  import Button from '@/common/button/Button.vue';
  import BuilderPriceCounter from '@/components/builder/components/BuilderPriceCounter.vue';

  export default {
    name: 'PizzaBuilder',
    components: {
      BuilderPriceCounter,
      Button, BuilderPizzaView, BuilderIngredientsSelector, BuilderSizeSelector, BuilderDoughtSelector,
    },
    data() {
      return {
        pizzaData: {
          name: '',
          dough: null,
          size: null,
          sauce: null,
          filling: {
            mushrooms: {},
            cheddar: {},
            salami: {},
            ham: {},
            ananas: {},
            bacon: {},
            onion: {},
            chile: {},
            jalapeno: {},
            olives: {},
            tomatoes: {},
            salmon: {},
            mozzarella: {},
            parmesan: {},
            blue_cheese: {},
          },
        },
        pizzaPriceData: {},
        isReadyToCook: false,
      };
    },
    watch: {
      pizzaData: {
        deep: true,
        handler() {
          this.getPriceData();
          this.checkReadyToCook();
        },
      },
    },
    methods: {
      getPriceData() {
        let fillingPrice = 0;
        for (let fil in this.pizzaData.filling) {
          fillingPrice += this.pizzaData.filling[fil]?.price ?? 0;
        }
        this.pizzaPriceData = {
          sizeMultiplier: this.pizzaData.size?.multiplier ?? 0,
          doughPrice: this.pizzaData.dough?.price ?? 0,
          saucePrice: this.pizzaData.sauce?.price ?? 0,
          ingredientPrice: fillingPrice,
        };
      },
      checkReadyToCook() {
        let ingredient = false;
        for (let fil in this.pizzaData.filling) {
          if (this.pizzaData.filling[fil]?.counter > 0) {
            ingredient = this.pizzaData.filling[fil]?.counter > 0;
            break;
          }
        }
        this.isReadyToCook = ingredient && this.pizzaData.name;
      },
    },
  };
</script>

<style scoped>

</style>
