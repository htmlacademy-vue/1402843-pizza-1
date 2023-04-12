<template>
  <div class="content__diameter">
    <div class="sheet">
      <h2 class="title title--small sheet__title">Выберите размер</h2>
      <div class="sheet__content diameter">
        <!--                  TODO: указать дефолтные значения для v-model-->
        <!--      TODO: в pizza.json временно добавлен value для size-->
        <SelectorItem
          v-for="size in pizza.sizes"
          :key="size.id"
          name="diameter"
          :data="size"
          @itemSelected="$emit('sizeSelected', $event)"
        >
        </SelectorItem>
      </div>
    </div>
  </div>
</template>

<script>
  import pizza from '@/static/pizza.json';
  import {SIZE} from '@/common/const/constants';
  import SelectorItem from '@/common/input/SelectorItem.vue';

  export default {
    name: 'BuilderSize',
    components: {SelectorItem},
    data() {
      return {
        pizza,
        SIZE,
      };
    },
  };
</script>

<style scoped>

</style>
