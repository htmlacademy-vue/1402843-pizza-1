<template>
  <div class="content__ingridients">
    <div class="sheet">
      <h2 class="title title--small sheet__title">
        Выберите ингридиенты
      </h2>

      <div class="sheet__content ingridients">
        <BuilderIngredientsSauce @sauceSelected="$emit('sauceSelected', $event)"></BuilderIngredientsSauce>
        <div class="ingridients__filling">
          <p>Начинка:</p>

          <BuilderIngredientsFilling @fillingSelected="$emit('fillingSelected', $event)"></BuilderIngredientsFilling>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import BuilderIngredientsSauce
    from '@/components/builder/components/BuilderIngredientsSauce.vue';
  import BuilderIngredientsFilling
    from '@/components/builder/components/BuilderIngredientsFilling.vue';

  export default {
    name: 'BuilderIngredients',
    components: {BuilderIngredientsFilling, BuilderIngredientsSauce},
  };
</script>

<style scoped>

</style>
