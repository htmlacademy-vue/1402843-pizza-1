<template>
  <ul class="ingridients__list">
    <li
      class="ingridients__item"
      v-for="ingredient in pizza.ingredients"
      :key="ingredient.id"
    >
      <!--      TODO: в pizza.json временно добавлен value для ingredients-->
      <ItemCounter
        :data="ingredient"
        counterType="ingridients"
        itemType="filling"
        :itemDraggable="true"
        :itemMaximumCount="3"
        @quantitySelected="$emit('fillingSelected', $event)"
      >
      </ItemCounter>
    </li>
  </ul>
</template>

<script>
  import pizza from '@/static/pizza.json';
  import {INGREDIENTS} from '@/common/const/constants';
  import ItemCounter from '@/common/input/ItemCounter.vue';

  export default {
    name: 'BuilderIngredientsFilling',
    components: {ItemCounter},
    data() {
      return {
        pizza,
        INGREDIENTS,
      };
    },
  };
</script>

<style scoped>

</style>
