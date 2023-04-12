<template>
  <div class="ingridients__sauce">
    <p>Основной соус:</p>

    <!--  TODO: указать дефолтные значения для v-model-->
    <!--    TODO: в pizza.json временно добавлен value для sauces-->
    <Radio
      v-for="sauce in pizza.sauces"
      :key="sauce.id"
      class="ingridients__input"
      name="sauce"
      :data="sauce"
      @itemSelected="$emit('sauceSelected', $event)"
    >
    </Radio>
  </div>
</template>

<script>
  import pizza from '@/static/pizza.json';
  import {SAUCE} from '@/common/const/constants';
  import Radio from '@/common/input/Radio.vue';

  export default {
    name: 'BuilderIngredientsSauce',
    components: {Radio},
    data() {
      return {
        pizza,
        SAUCE,
      };
    },
  };
</script>

<style scoped>

</style>
