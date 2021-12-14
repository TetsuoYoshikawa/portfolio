<template>
  <div class="home">
    <img class="top-eyecatch" src="../assets/eyecatch.jpg"/>
    <h1 class="media__fv-ttl">
        Portfolio
      <div class="small">Web Engineer</div>
    </h1>
    <div class="about" id="about">
      <div>
        <div class="content-title">
          <h2>ABOUT</h2>
        </div>
        <div class="profile flex-2">
          <div class="profile-img">
            <p>
            </p>
          </div>
          <div class="profile-detail">
            <ul>
              <li>名前：吉川 哲生</li>
              <li>出身：兵庫県</li>
              <li>特技：ラテアート</li>
            </ul>
            <p class="text">
              はじめまして。平成9年生まれ24歳エンジニアのてつおと申します。大手電機メーカーで、製造課として働いていた経歴があり、ものづくりは昔から大好きです。社内大会で、近畿地方3位まで行き、技術指導者として、東京で勤めたこともあります。モノづくりを通して新しい技術を生み出せればと思いエンジニアになりました。
              また、カフェで働いていた経験があり、ラテアートが得意です。相当自信あります。
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="skill" id="skill">
      <div class="content-title">
        <h1>SKILL</h1>
      </div>
      <div class="skill-box flex-2">
        <div class="skill-card flex-2" v-for="skill in skill" :key="skill.id">
          <div class="skill-icon">
            <img :src="'https://tetsuoyoshikawa.s3.ap-northeast-3.amazonaws.com/' + skill.image">
          </div>
          <div class="skill-desc">
            <h3>{{skill.name}}</h3>
            <div class="rating">
              <div v-if="skill.skill === 5">
                <div>★★★★★</div>
              </div>
              <div v-else-if="skill.skill === 4">
                <div>★★★★☆</div>
              </div>
              <div v-else-if="skill.skill === 3">
                <div>★★★☆☆</div>
              </div>
              <div v-else-if="skill.skill === 2">
                <div>★★☆☆☆</div>
              </div>
              <div v-else-if="skill.skill === 1">
                <div>★☆☆☆☆</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="portfolio" id="portfolio">
      <div class="content-title">
        <h1>Portfolio</h1>
      </div>
      <div class="flex">
        <div v-for="portfolio in portfolio" :key="portfolio.id">
          <div class="portfolio-card">
            <a :href="portfolio.url" class="portfolio-colum">
              <img :src="'https://tetsuoyoshikawa.s3.ap-northeast-3.amazonaws.com/' + portfolio.image" class="portfolio-image">
              <p class="portfolio-tag">
                {{portfolio.name}}
              </p>
            </a>
            <div class="portfolio-tags">
              <div class="portfolio-tags__inner">
                <p>フロントエンド:HTML,CSS,JavaScript（Vue.js）</p>
                <p>バックエンド:PHP（Laravel）</p>
                  <p>作成期間:{{portfolio.created}}</p>
                  <p>
                  <a>github:</a>
                  <a class="github" :href="portfolio.github_front">フロントエンド</a>
                </p>
                <p>
                  <a>github:</a>
                  <a class="github" :href="portfolio.github_api">バックエンド</a>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Contact />
    <Footer />
  </div>
</template>

<script>
import axios from "axios";
import Contact from "../components/Contact.vue";
import Footer from "../components/Footer.vue";
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
  },
  components:{
    Contact,
    Footer
  }
}
</script>

<style scoped>
/*------------------------*/
/*         article        */
/*------------------------*/
/* article.html */
.article-nav {
  background: #fff;
  text-align: center;
  width: 100%;
}
.header-flex {
  justify-content: center;
}
.header-flex li {
  margin: 0 20px 20px;
}
.article-logo .magazine-subtitle {
  font-size: 12px;
}
#top-header.article-nav {
  background: #fff;
}
/* eyecatch */
.eyecatch {
  margin: 0 auto;
}
.top-eyecatch {
  height: 100vh;
  background-size: cover;
  background-position: center;
  position: relative;
  width: 100%;
}
.media__fv-ttl {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  font-size: 100px;
  text-align: center;
  color: #fff;
  width: 80%;
}
.small {
  font-size: 50px;
}
.about {
  width: 100%;
  margin: 100px 0 150px 0;
}
.content-title {
  text-align: center;
  font-size: 50px;
  line-height: 50px;
  margin-bottom: 30px;
}
.profile {
  width: 100%;
}
.profile-img {
  width: 30%;
  margin-left: 100px;
  border-radius: 10px;
}
.profile-img p {
  width: 300px;
  height: 300px;
}
.profile-detail {
  margin-left: 100px;
  font-size: 20px;
}
.profile-detail li{
  padding-bottom: 20px;
}
.text {
  width: 85%;
}
/* new */
.text-content {
  min-height: 130px;
  position: relative;
  max-height: 120px;
  width: 100%;
}
.skill {
  margin: 100px auto;
  width: 70%;
}
.skill-box {
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 50px;
  margin-left: 0%;
  background-color: white;
}
.skill-card {
  display: flex;
  flex-basis: 40%;
  margin: 20px 0;
  font-size: 20px;
  border-bottom: 1px solid #999;
}
.skill-icon img {
  height: 60px;
  width: 60px;
}
.skill-desc {
  margin: 0 20px;
}
.skill-text {
  font-size: 15px;
}
/*------------------------*/
/*        category        */
/*------------------------*/
.category-type {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  font-size: 30px;
  color: #fff;
}
.category-colum {
  margin-top: 0;
  margin-left: 0;
  background-color: white;
}
.portfolio-card {
  width: 100%;
  margin: 10px 20px 10px 20px;
  padding-bottom: 10px;
  background: #fff;
  box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.6);
}
.portfolio-colum {
  display: block;
  position: relative;
  max-height: 400px;
  box-sizing: border-box;
  padding-bottom: 10px;
}
.portfolio-image {
  height: 200px;
}
.portfolio-tag {
  text-align: center;
  background: #000;
  opacity: 0.6;
  padding: 5px;
  position: absolute;
  top: 0px;
  left: 0px;
  color: #fff;
  font-size: 14px;
  min-width: 100px;
}
.portfolio__date,
.portfolio-tags__inner {
  font-size: 12px;
  padding-bottom: 10px;
  margin-left: 10px;
}
.portfolio-tags__inner p {
  margin-bottom: 10px;
}

@media screen and (max-width: 960px) {
  .magazine-colum {
    width: 43%;
  }
}
/* 768以下の時のスタイル */
@media screen and (max-width: 768px) {
  .container-top {
    padding-bottom: 70px;
    width: 100%;
  }
  /* contact */
  label {
    display: block;
  }
  .form > div {
    margin: 0 auto;
  }
  input,
  textarea {
    width: 100%;
  }
  .magazine-colum {
    width: 80%;
  }
  .magazine-colum.top-interview {
    width: 80%;
  }
  .cta-text {
    width: 90%;
    margin-bottom: 30px;
  }
  .top-eyecatch {
    margin: 0;
  }
  .single-eyecatch img {
    height: auto;
    object-fit: contain;
  }
  .single-title {
    font-size: 25px;
    margin-bottom: 20px;
    line-height: 1.2;
  }
  .main-text h2 {
    font-size: 23px;
    border-bottom: 3px solid #707070;
    padding: 10px;
    margin: 20px 0;
  }
  .main-text h3 {
    font-size: 18px;
    border-bottom: 2px solid #707070;
    border-left: 10px solid #707070;
    border-top: 2px solid #707070;
    border-right: 2px solid #707070;
    padding: 10px;
    margin: 20px 0 20px 0;
  }
  .main-text h4 {
    font-size: 15px;
    border-bottom: 1px solid #707070;
    border-left: 10px solid #707070;
    padding: 10px;
    margin: 20px 0 20px 0;
  }
  .single-container {
    margin: 0 15px;
  }
  .single-container p {
    font-size: 14px;
  }
  .eyecatch {
    padding: 0;
  }
  .single-category-tag {
    top: -32px;
  }
  .single-container {
    padding: 15px;
  }
  .news-title {
    display: block;
    margin: 10px;
  }
  .news-list {
    padding: 8px 0;
  }
  .sidebar {
    width: 90%;
  }
  .page-title__h1 {
    font-size: 25px;
    line-height: 1.2;
  }
}

</style>
