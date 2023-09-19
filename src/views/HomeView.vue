<script setup lang="ts">
import { ref } from 'vue'
import type { RecommendStatus } from '../types'
import { restaurantStatusList } from '../constants'

interface Restaurant {
  name?: string
  status?: RecommendStatus
  dishes?: Dish[]
}

interface Dish {
  name: string
  halal?: Halal
  status?: RecommendStatus
}

type Halal = 'halal' | 'non halal'

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({
  status: 'Want to Try'
})

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    status: newRestaurant.value.status,
    dishes: []
  })
}
</script>

<template>
  <main>
    <pre>
      {{ newRestaurant }}
    </pre>
    <!-- Create form to add restauran list -->
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input id="restaurant-name" v-model="newRestaurant.name" type="text" />
      </div>
      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <select name="restaurant-status" id="restaurant-status" v-model="newRestaurant.status">
          <option v-for="status in restaurantStatusList" :value="status">
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant.name }} - {{ restaurant.status }}
      </li>
    </ul>
  </main>
</template>
