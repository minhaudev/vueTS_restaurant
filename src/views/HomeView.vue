<script setup lang="ts">
import { ref } from 'vue'
type DishType = {
  name: string
}
type RestaurantStatus = 'Want to Try' | 'Recommended' | 'Do Not Recommend' | 'Must Try'
const statusList = ['Want to Try', 'Recommended', 'Do Not Recommend', 'Must Try']
interface Restaurant {
  name?: string
  address?: string
  status?: RestaurantStatus
  dishes?: DishType[]
}
const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})

const addRestaurant = () => {
  if (newRestaurant.value.name) {
    restaurantList.value.push({ ...newRestaurant.value })
    // Reset lại form sau khi thêm nhà hàng
    ;(newRestaurant.value.name = ''),
      (newRestaurant.value.address = ''),
      (newRestaurant.value.status = 'Want to Try'),
      (newRestaurant.value.dishes = [])
  }
}
</script>

<template>
  <main class="home">
    <pre> {{ newRestaurant }} </pre>
    <form @submit.prevent="addRestaurant">
      <label for="restaurant-name">Restaurant name </label>
      <input id="restaurant-name" v-model="newRestaurant.name" type="text" />

      <label for="restaurant-status">Restaurant status </label>

      <select name="restaurant-status" id="restaurant-status" v-model="newRestaurant.status">
        <option v-for="(status, index) in statusList" :key="index" :value="status">
          {{ status }}
        </option>
      </select>

      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="(restaurant, index) in restaurantList" :key="index">
        {{ restaurant.name }} - {{ restaurant.status }}
      </li>
    </ul>
  </main>
</template>

<style scoped>
.home {
  font-size: 38px;
}
button {
  background-color: aqua;
  padding: 16px 8px;
  font-weight: bold;
}
label {
  font-size: 30px;
}
input {
  font-size: 20px;
  height: 50px;
  width: 100%;
}
select {
  font-size: 20px;
  width: 100%;
  height: 50px;
}
li {
  font-size: 28px;
}
@media (min-width: 1024px) {
  .home {
    min-height: 100vh;
  }
}
</style>
