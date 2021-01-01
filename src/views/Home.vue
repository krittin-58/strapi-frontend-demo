<template>
  <div class="home">
    <div v-if="error">
      {{ error }}
    </div>
    <ul v-else>
      <li v-for="restaurant in restaurants" :key="restaurant.id">
        {{ restaurant.name }}
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {},
  data() {
    return {
      restaurants: [],
      error: null,
      headers: {
        'Content-Type': 'application/json',
      },
    };
  },

  async mounted() {
    try {
      const response = await fetch('http://localhost:1337/restaurants', {
        method: 'GET',
        headers: this.headers,
      }).then(this.parseJSON);
      this.restaurants = response;
    } catch (error) {
      this.error = error;
    }
  },

  methods: {
    parseJSON(resp) {
      return (resp.json ? resp.json() : resp);
    },

    // checkStatus(resp) {
    //   if (resp.status >= 200 && resp.status < 300) {
    //     return resp;
    //   }
    //   return this.parseJSON(resp).then((resp) => {
    //     throw resp;
    //   });
    // },

    getRestaurants() {
      fetch('http://localhost:1337/restaurants', {
        method: 'GET',
        headers: this.headers,
      })
        .then((response) => response.json())
        .then((data) => console.log(data));
    },
  },
};
</script>
