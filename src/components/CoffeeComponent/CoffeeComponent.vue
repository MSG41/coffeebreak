<template>
  <div>
    <div class="options">
      <div
        v-for="(option, index) in coffeeOptions"
        :key="index"
        :style="{ '--i': index + 1 }"
        @click="selectOption(option)"
        :class="{ selected: option === selectedOption }"
      >
        {{ option }}
      </div>
    </div>

    <div class="wrapper">
      <div class="shadow"></div>
      <div class="title">{{ selectedOption }}</div>
      <div class="cup" :class="[formatOption, 'cup']" @click="selectRandomOption">
        <div class="contents">
          <div class="gelato">gelato</div>
          <div class="foam">milk foam</div>
          <div class="cream">cream</div>
          <div class="steamed-milk">steamed milk</div>
          <div class="milk">milk</div>
          <div class="chocolate">chocolate</div>
          <div class="sugar">sugar</div>
          <div class="whiskey">whiskey</div>
          <div class="water">water</div>
          <div class="coffee">coffee</div>
          <div class="espresso">espresso</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { ref, computed } from 'vue'

export default {
  name: 'CoffeeComponent',
  setup() {
    const coffeeOptions = ref<string[]>([
      'Black',
      'Flat White',
      'Latte',
      'Cappuccino',
      'Americano',
      'Espresso',
      'Doppio',
      'Cortado',
      'Macchiato',
      'Mocha',
      'Affogato',
      'Con Panna',
      'Irish',
      'Cafe Au Lait'
    ])

    const selectedOption = ref<string>(coffeeOptions.value[0])

    const selectOption = (option: string) => {
      selectedOption.value = option
    }

    const selectRandomOption = () => {
      const randomIndex = Math.floor(Math.random() * coffeeOptions.value.length)
      selectedOption.value = coffeeOptions.value[randomIndex]
    }

    const formatOption = computed(() => {
      return selectedOption.value.toLowerCase().replace(/\s/g, '-')
    })

    return {
      coffeeOptions,
      selectedOption,
      selectRandomOption,
      formatOption,
      selectOption
    }
  }
}
</script>

<style>
@import './CoffeeStyle.css';
</style>
