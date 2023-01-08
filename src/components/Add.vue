<template>

  <Header/>

  <h1>Hello {{name}}, welcome to Add Restaurant Page</h1>

  <form action="" class="add">
    <input type="text" name="name" placeholder="Enter name " v-model="restaurant.name">
    <input type="text" name="address" placeholder="Enter address " v-model="restaurant.address">
    <input type="text" name="contact" placeholder="Enter contact " v-model="restaurant.contact">
    <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>
  </form>

</template>


<script>

import axios from 'axios'

import Header from "@/components/Header.vue";
  export default {
    name : 'Add-main',

    data(){
      return {
        name: '',
        restaurant: {
          name: '',
          address: '',
          contact: ''
        }
      }
    },

    components:{
      Header
    },


    //if user-info NOT IN localStorage redirect to SignUp
    mounted()
    {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;


      if (!user)
      {
        this.$router.push({name:'SignUp'})
      }




    },

    methods: {
      async addRestaurant()
      {

        let result = await axios.post("http://localhost:3000/restaurant", {
          'name' : this.restaurant.name,
          'address' : this.restaurant.address,
          'contact' : this.restaurant.contact,
        });

        if(result.status == 201)
        {
          this.$router.push({name:'Home'})
        }

        console.log(result)
      }
    }
  }

</script>