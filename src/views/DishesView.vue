<script setup lang="ts">
import { ref } from 'vue'
import type { RecommendStatus } from '../types'
import { restaurantStatusList } from '../constants'

interface Dish {
  name?: string
  halal?: Halal
  status?: RecommendStatus
}

type Halal = 'halal' | 'non halal'

const dishList = ref<Dish[]>([])
const newDishes = ref<Dish>({
  status: 'Want to Try'
})

function addDish() {
  dishList.value.push({
    name: newDishes.value.name,
    status: newDishes.value.status
  })
}
</script>

<template>
  <main>
    <pre>
      {{ newDishes }}
    </pre>
    <!-- Create form to add restauran list -->
    <form @submit.prevent="addDish">
      <div>
        <label for="dishes-name">Dishes Name</label>
        <input id="dishes-name" v-model="newDishes.name" type="text" />
      </div>
      <div>
        <label for="dishes-status">Dishes Status</label>
        <select name="dishes-status" id="dishes-status" v-model="newDishes.status">
          <option v-for="status in restaurantStatusList" :value="status">
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add Dish</button>
    </form>
    <ul>
      <li v-for="dish in dishList" :key="dish.name">{{ dish.name }} - {{ dish.status }}</li>
    </ul>
  </main>
</template>
