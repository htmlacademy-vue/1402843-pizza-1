<template>
  <main class="content">
    <PizzaBuilder></PizzaBuilder>
  </main>
</template>

<script>
  import PizzaBuilder from '@/components/builder/PizzaBuilder.vue';

  export default {
    name: 'Main',
    components: {PizzaBuilder},
  };
</script>

<style scoped>

</style>
