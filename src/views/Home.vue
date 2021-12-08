<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import axios from "axios";
export default{
  data(){
    return{
      portfolio:[],
      skill:[]
    }
  },
  methods:{
    async getPortfolio(){
      await axios
        .get("http://127.0.0.1:8000/api/portfolio")
        .then((response) => {
          this.portfolio = response.data.data;
        })
    },
    async getSkill(){
      await axios
        .get("http://127.0.0.1:8000/api/skill")
        .then((response) => {
          this.skill = response.data.data;
        })
    },
  },
  created(){
    this.getPortfolio();
    this.getSkill();    
  }
}
</script>
