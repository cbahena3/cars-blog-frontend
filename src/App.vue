<script>
  import axios from "axios";
  export default {
    data: function () {
      return {
        cars: [],
      };
    },
    created: function () {
      this.indexCars();
    },
    methods: {
      indexCars: function () {
        axios.get("/cars.json").then((response) => {
          console.log("cars index", response);
          this.cars = response.data;
        });
      },
    },
  };
</script>

<template>
  <div class="home">
    <h1>All Cars</h1>
    <div v-for="car in cars" v-bind:key="car.id">
      <h2>{{ car.title }}</h2>
      <img v-bind:src="car.image" v-bind:alt="car.make" />
      <p>Description: {{ car.description }}</p>
      <p>Make: {{ car.make }}</p>
      <p>Model: {{ car.model }}</p>
      <p>Color: {{ car.color }}</p>
      <p>Year: {{ car.year }}</p>
    </div>
  </div>
</template>

<style></style>