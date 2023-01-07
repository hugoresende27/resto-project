<template>

  <img alt="Me" src="../assets/logo.jpg" class="logo">
  <h1>
    Sign Up
  </h1>

  <div class="register">
    <input type="text" v-model="name" placeholder="Enter Name"/>
    <input type="email" v-model="email"  placeholder="Enter Email"/>
    <input type="password"  v-model="password"  placeholder="Enter Password"/>
    <button v-on:click="signUp">Sign Up</button>

    <p>
      <router-link to="/login">Go to Login</router-link>
    </p>
  </div>

</template>


<script>

import axios from 'axios'
  export default {

    name:'SignUp',

    data()
    {
      return {
        name : '',
        email: '',
        password: ''
      }
    },

    methods: {
      async signUp()
      {
        // console.warn(this.name, this.email, this.password)
        let result = await axios.post("http://localhost:3000/users", {
          'name' : this.name,
          'email' : this.email,
          'password' : this.password,
        });


        console.log (result);

        if (result.status === 201)
        {
          // alert ("sign-up done");

          //save user-info in localStorage
          localStorage.setItem("user-info", JSON.stringify(result.data))

          this.$router.push({name:'Home'})
        }
      }
    },

    //if user-info in localStorage redirect to Home
    mounted()
    {
      let user = localStorage.getItem("user-info");

      if (user)
      {
        this.$router.push({name:'Home'})
      }

    }

  }

</script>


<style>





</style>
