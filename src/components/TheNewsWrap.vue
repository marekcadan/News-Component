<template>
    <div class="flexbox">
      <div class="news" v-for="newsItem in news" :key="newsItem.id" @click="newsOpen(newsItem.url)">
        <div class="image"><img :src="newsItem.image" class="image-fit"></div>
        <div class="title">{{ newsItem.title }}</div>
        <div class="date-time">{{ newsItem.date }} | {{ newsItem.time }} read</div>
      </div>
    </div>
    <div class="bt-center">
      <button class="news-button" onclick="window.open('https://www.pipelife.com/service/news-and-projects.html', '_self');">
          see all News & Projects
      </button>
    </div>
</template>

<script>
import NewsData from "../json/news.json";
export default {
  data() {
    return {
      myNews: NewsData,
      news: NewsData,
      width: window.innerWidth,
    };
  },
  created() {
    this.news = this.myNews.slice(0, 5);
    window.addEventListener("resize", this.onResize);
  },
  destroyed() {
    window.removeEventListener("resize", this.onResize);
  },
  methods: {
    newsOpen(url) {
      window.open(url, "_self");
    },
    onResize(e) {
      this.width = window.innerWidth;
      if (this.width > 995) {this.news = this.myNews.slice(0, 5);}
      if (this.width <= 995 && this.width >= 630) {this.news = this.myNews.slice(0, 4);}
      if (this.width < 630) {this.news = this.myNews.slice(0, 3);}
    },
  },
};
</script>

<style scoped>
.flexbox {
  display: flex;
  padding: 5px 20px;
}

.news {
  width: 50%;
  min-width: 190px;
  cursor: pointer;
}

.image {
  display: flex;
  justify-content: center;
  padding-top: 20px;
}

.image-fit{
  height: 100%;
  width: 90%;
  object-fit: cover;
}

.title {
  color: #003087;
  font-size: 1.1rem;
  font-weight: 750;
  width: 80%;
  padding: 15px 10% 10px 10%;
}

.date-time {
  width: 80%;
  padding-left: 10%;
  font-weight: 100;
  font-size: 0.9rem;
}

.bt-center {
  display: flex;
  justify-content: center;
}

.news-button {
  background-color: #003087;
  border: 0;
  border-radius: 30px;
  color: white;
  padding: 16px 32px;
  text-align: center;
  font-size: 16px;
  font-weight: 650;
  margin: 30px 0px;
  transition-duration: 0.2s;
  cursor: pointer;
}

.news-button:hover {
  background-color: #41b6e6;
}

@media (max-width: 995px) {
  .flexbox {
    flex-wrap: wrap;
  }
}

@media (max-width: 630px) {
  .flexbox {
    flex-wrap: wrap;
  }

  .news {
    width: 100%;
  }
}

</style>