<template>

  <Header/>

  <h1>Hello {{ name }}, welcome to Home Page</h1>
  <table border="1">
    <tr>
      <td>ID </td>
      <td>NAME </td>
      <td>ADDRESS </td>
      <td>CONTACT </td>
      <td>ACTIONS </td>
      <td>DELETE </td>
    </tr>

    <tr v-for="item in restaurant"  v-bind:key="item.id" >
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.address}}</td>
      <td>{{item.contact}}</td>
      <td><router-link :to="'/update/'+item.id">Update</router-link></td>
      <td>
      <button v-on:click="deleteRestaurant(item.id)">Delete</button>
      </td>
    </tr>
  </table>

</template>


<script>

import Header from "@/components/Header.vue";
import axios from 'axios';

  export default {
    name: 'Home-main',

    data() {
      return {
        name: '',
        restaurant: []
      }
    },

    components: {
      Header
    },

    //if user-info NOT IN localStorage redirect to SignUp
    async mounted() {
      await this.loadData()
    },

    methods: {
      async deleteRestaurant(id) {

        const result = await axios.delete('http://localhost:3000/restaurant/' + id);
        if (result.status === 200) {
          this.loadData()
        }
      },

      async loadData() {
        let user = localStorage.getItem("user-info");

        this.name = JSON.parse(user).name;

        if (!user) {
          this.$router.push({name: 'SignUp'})
        }

        let result = await axios.get('http://localhost:3000/restaurant/');

        console.log(result.data);

        this.restaurant = result.data
      }
    }
  }

</script>


<style>
td{
  width: 160px;
  height: 50px;
}

</style>