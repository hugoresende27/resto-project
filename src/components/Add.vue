<template>

  <Header/>

  <h1>Hello {{name}}, welcome to Add Restaurant Page</h1>

</template>


<script>

import Header from "@/components/Header.vue";
  export default {
    name : 'Add-main',

    data(){
      return {
        name: ''
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
      console.log(this.name)

      if (!user)
      {
        this.$router.push({name:'SignUp'})
      }

    }
  }

</script>