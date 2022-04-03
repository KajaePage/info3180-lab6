<template>
   <ul class="news__list">
    <div class="row">
       <div class="col-md-4 mb-5" v-for="article in articles"> 
        <div class="card  h-100" style="border-bottom : solid green;">
          <img class="card-img-top img-fluid images_" v-bind:src= article.urlToImage  alt="Article image">
          <div class="card-body">
            <h3 class="card-title" style="text-align: left;">{{ article.title }}</h3>
            <p class="card-text" style="text-align: left;">{{article.description}}</p>
            <br>
          </div>
        </div>
      </div>
      </div>
    </ul>
</template>
<script>
export default {
    data() {
        return {
 articles: []
 }
    },
    created() {
        let self = this;
 fetch('https://newsapi.org/v2/top-headlines?country=us',
{
 headers: {
 'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
 }
})
 .then(function(response) {
 return response.json();
 })
 .then(function(data) {
 console.log(data);
 self.articles = data.articles;
 });
 }
};
</script>