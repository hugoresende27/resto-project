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
    </tr>

    <tr v-for="item in restaurant"  v-bind:key="item.id" >
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.address}}</td>
      <td>{{item.contact}}</td>
      <td><router-link :to="'/update/'+item.id">Update</router-link></td>
    </tr>
  </table>

</template>


<script>

import Header from "@/components/Header.vue";
import axios from 'axios';

  export default {
    name : 'Home-main',

    data(){
      return {
        name: '',
        restaurant: []
      }
    },

    components:{
      Header
    },

    //if user-info NOT IN localStorage redirect to SignUp
    async mounted()
    {
      let user = localStorage.getItem("user-info");

      this.name = JSON.parse(user).name;

      if (!user)
      {
        this.$router.push({name:'SignUp'})
      }

      let result = await axios.get('http://localhost:3000/restaurant');

      console.log(result.data);

      this.restaurant = result.data


    }
  }

</script>


<style>
td{
  width: 160px;
  height: 50px;
}

</style>