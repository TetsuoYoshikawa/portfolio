<template>
  <div class="home">
    <div class="portfolio" v-for="portfolio in portfolio" :key="portfolio.id">
      <p>{{portfolio.id}}</p>
      <p>{{portfolio.name}}</p>
      <p>{{portfolio.created}}</p>
      <p>{{portfolio.detail}}</p>
      <p>{{portfolio.difficulties}}</p>
      <a>{{portfolio.github_front}}</a>
      <a>{{portfolio.github_api}}</a>
      <p>{{portfolio.solutions}}</p>
      <a>{{portfolio.url}}</a>
    </div>
    <div class="skill" v-for="skill in skill" :key="skill.id">
      <p>{{skill.id}}</p>
      <p>{{skill.name}}</p>
      <p>{{skill.skill}}</p>
    </div>
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
