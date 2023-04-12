<template>
  <div class="content__dough">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите тесто</h2>

      <div class="sheet__content dough">
        <!--                  TODO: указать дефолтные значения для v-model-->
        <!--      TODO: в pizza.json временно добавлен value для dough-->
        <SelectorItem
          v-for="dough in pizza.dough"
          :key="dough.id"
          name="dough"
          :data="dough"
          @itemSelected="$emit('doughSelected', $event)"
        >
        </SelectorItem>
      </div>
    </div>
  </div>
</template>

<script>
  import pizza from '@/static/pizza.json';
  import {DOUGHT} from '@/common/const/constants';
  import SelectorItem from '@/common/input/SelectorItem.vue';

  export default {
    name: 'BuilderDought',
    components: {SelectorItem},
    data() {
      return {
        pizza,
        DOUGHT,
      };
    },
  };
</script>

<style scoped>

</style>
