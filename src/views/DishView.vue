<script setup lang="ts">
import { ref } from 'vue'

enum RestaurantStatus {
  WantToTry = 'Want to Try',
  Recommended = 'Recommended',
  DoNotRecommend = 'Do Not Recommend',
  MustTry = 'Must Try'
}
// type RestaurantStatus = 'Want to Try' | 'Recommended' | 'Do Not Recommend' | 'Must Try'
// const statusList = ['Want to Try', 'Recommended', 'Do Not Recommend', 'Must Try']
type Diet = 'vegetarian' | 'vegan' | 'gluten-free'

interface Dish {
  name?: string
  status?: RestaurantStatus
  diet?: Diet
}
const restaurantList = ref<Dish[]>([])

const newDishes = ref<Dish>({})

const addRestaurant = () => {
  if (newDishes.value.name) {
    restaurantList.value.push({ ...newDishes.value })
    // Reset lại form sau khi thêm nhà hàng
    newDishes.value.name = ''
    newDishes.value.status = RestaurantStatus.WantToTry
  } else {
    alert('chưa nhập tên món ăn!')
  }
}
</script>

<template>
  <main class="home">
    <pre> {{ newDishes }} </pre>
    <form @submit.prevent="addRestaurant">
      <label for="dish-name">Restaurant name </label>
      <input id="dish-name" v-model="newDishes.name" type="text" />

      <label for="restaurant-status">Restaurant status </label>

      <select name="restaurant-status" id="restaurant-status" v-model="newDishes.status">
        <option
          v-for="(status, index) in Object.values(RestaurantStatus)"
          :key="index"
          :value="status"
        >
          {{ status }}
        </option>
      </select>
      <label for="dish-diet">Restaurant Diet </label>
      <input id="dish-diet" v-model="newDishes.diet" type="text" />

      <button type="submit">ADD DISH</button>
    </form>
    <ul>
      <li v-for="(restaurant, index) in restaurantList" :key="index">
        {{ restaurant.name }} - {{ restaurant.status }} - {{ restaurant.diet }}
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
