<template>

  <Header/>

  <h1>Hello {{name}}, welcome to Update Restaurant Page</h1>

  <form action="" class="add">
    <input type="text" name="name" placeholder="Enter name " v-model="restaurant.name">
    <input type="text" name="address" placeholder="Enter address " v-model="restaurant.address">
    <input type="text" name="contact" placeholder="Enter contact " v-model="restaurant.contact">
    <button type="button" v-on:click="updateRestaurant">Update {{restaurant.name}} Restaurant</button>
  </form>

</template>


<script>

import axios from 'axios'

import Header from "@/components/Header.vue";
  export default {
    name : 'Update-main',

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
    async mounted()
    {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;


      if (!user)
      {
        this.$router.push({name:'SignUp'})
      }


      const result = await axios.get('http://localhost:3000/restaurant/'+this.$route.params.id);
      // console.log(this.$route.params.id)
      console.log(result)

      //fill property auto with bind .data
      this.restaurant = result.data




    },

    methods: {
      async updateRestaurant()
      {

        const result = await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id, {
          'name' : this.restaurant.name,
          'address' : this.restaurant.address,
          'contact' : this.restaurant.contact,
        });

        if(result.status === 200)
        {
          this.$router.push({name:'Home'})
        }

        console.log(this.restaurant)
      }
    }
  }

</script>