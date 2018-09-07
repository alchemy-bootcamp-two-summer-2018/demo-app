<template>
  <div>
    <h2>I am the Restaurants component</h2>
    <pre v-if="error">{{ error }}</pre>
    <ul v-if="restaurants">
      <li
        v-for="restaurant in restaurants"
        :key="restaurant.id"
      >
        <strong>{{ restaurant.name }}</strong>
        {{ restaurant.address.street }}
      </li>
    </ul>
  </div>
</template>

<script>
import { getRestaurants } from '../services/api';

export default {
  data() {
    return {
      restaurants: null,
      error: null
    };
  },
  created() {
    // if this wasn't in created, we'd need to reset error
    // this.error = null;
    getRestaurants()
      .then(restaurants => {
        this.restaurants = restaurants;
      })
      .catch(err => {
        this.error = err;
      });
  }

};

</script>

<style scoped>
pre {
  color: red;
}
</style>
