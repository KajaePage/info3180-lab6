<template>
<form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
 <div class="input-group mx-sm-3 mb-2">
 <label class="visually-hidden" for="search">Search</label>
 <input type="search" name="search" v-model="searchTerm"
id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
search term here" />
 <button class="btn btn-primary mb-2">Search</button>
 </div>
 <p>You are searching for {{ searchTerm }}</p>
 </form>
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
 articles: [],
 searchTerm: ''
 }
    },
 methods: {
 searchNews() {
 let self = this;
 fetch('https://newsapi.org/v2/everything?q='+ self.searchTerm + '&language=en', {
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
 }
};
</script>