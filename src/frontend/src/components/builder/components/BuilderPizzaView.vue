<template>
  <div>
    <label class="input">
      <span class="visually-hidden">Название пиццы</span>
      <input
        type="text"
        name="pizza_name"
        placeholder="Введите название пиццы"
        v-model="pizza_name"
        required
        @input="$emit('onInput', pizza_name)"
      />
    </label>
    <div class="content__constructor">
      <div
        class="pizza"
        :class="getFoundationClass">
        <div
          class="pizza__wrapper"
          @drop.stop="onDrop"
          @dragover.prevent
          @dragenter.prevent
        >
          <template v-if="classNames.length">
            <div
              v-for="element in classNames"
              class="pizza__filling"
              :class="element"
              :key="element"
            >
            </div>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import {DATA_TRANSFER_TEXT_TYPE} from '@/common/const/constants';
  import EventBus from '@/services/eventBus';

  export default {
    name: 'BuilderPizzaView',
    props: {
      pizzaConsist: {
        type: Object,
        required: true,
      },
    },
    data() {
      return {
        pizza_name: '',
        classNames: [],
      };
    },
    computed: {
      getFoundationClass() {
        return `pizza--foundation--${this.pizzaConsist.dough?.value ?? 'light'}-${this.pizzaConsist.sauce?.value ?? 'tomato'}`;
      },

    },
    watch: {
      pizzaConsist: {
        deep: true,
        handler() {
          this.getFillingElements();
        },
      },
    },
    methods: {
      onDrop({dataTransfer}) {
        const addedIngredient = dataTransfer.getData(DATA_TRANSFER_TEXT_TYPE);
        if (addedIngredient) {
          EventBus.$emit(`add-${addedIngredient}`);
        }
      },
      getFillingElements() {
        let classNames = [];
        for (let fil in this.pizzaConsist.filling) {
          let componentClassName;
          if (this.pizzaConsist.filling[fil]?.counter > 0) {
            componentClassName = `pizza__filling--${this.pizzaConsist.filling[fil].value}`;
            if (this.pizzaConsist.filling[fil].counter > 1) {
              componentClassName = `${componentClassName} pizza__filling--${this.pizzaConsist.filling[fil].counter === 2 ? 'second' : 'third'}`;
            }
            classNames.push(componentClassName);
          }
        }
        this.classNames = classNames;
      },
    },
  };
</script>

<style scoped>

</style>
