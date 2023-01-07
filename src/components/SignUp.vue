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
          alert ("sign-up done");
          localStorage.setItem("user-info", JSON.stringify(result.data))

          this.$router.push({name:'Home'})
        }
      }
    }

  }

</script>


<style>

.logo{
  width: 100px;
  height: 100px;
  border-radius: 50%;
}

.register input{
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid darkblue;
  border-radius: 10px;
}

.register button {
  width: 320px;
  height: 40px;
  border: 1px solid darkblue;
  background-color: darkblue;
  color: white;
  cursor: pointer;
  border-radius: 10px;
}



</style>
