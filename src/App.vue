<script>
  import axios from "axios";
  export default {
    data: function () {
      return {
        cars: [],
        currentCar: {}
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
      showCar: function (car) {
       this.currentCar = car;
       document.querySelector("#car-details").showModal();
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
      <button v-on:click="showCar(car)">More Car Info</button>
    </div>
    <dialog id="car-details">
       <form method="dialog">
         <h1>Car info</h1>
         <p>Title: {{ currentCar.title }}</p>
         <img :src="currentCar.image" alt="Car Image">
         <p>Description: {{ currentCar.description }}</p>
         <p>Make: {{ currentCar.make }}</p>
         <p>Model: {{ currentCar.model }}</p>
         <p>Color: {{ currentCar.color }}</p>
         <p>Year: {{ currentCar.year }}</p>
         <button>Close</button>
       </form>
     </dialog>
  </div>
</template>

<style></style>