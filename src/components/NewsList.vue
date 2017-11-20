<template>
  <div class="newslist">
    <div class="jumbotron">

      <h1>The Guardian News</h1>
      <button class="btn btn-primary" v-on:click="updateSource">Refresh</button>

    </div>
    <div class="container">

      <ul class="media-list">
        <li class="media" v-for="article in articles">

          <div class="media-body" >
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{article.title}}</a>
            </h4>
           <!-- <p>{{article.description}}</p>-->
          </div>

        </li>
      </ul>

    </div>

  </div>
</template>

<script>
  export default {
    data () {
      return {
        articles: []
      }
    },
    methods: {
      updateSource: function (){
        console.log("Trying to update...");
        this.$http.get('https://newsapi.org/v1/articles?source=the-guardian-uk&apiKey=7573228af0da456b98c14efdbf5c75d6')
          .then(response =>{
            this.articles = response.data.articles;
            console.log("UPDATED");
          }).catch(function (e) {
            alert("Sorry, we could find news for you. PLease try again later")
            console.log("EXCEPTION");
        })
      }
    },
    created: function(){
      this.updateSource(this.source)
    }
  }
</script>

<style scoped>
  .media {
    border-top: 1px solid lightgray;
    padding-top: 20px;
  }
  .jumbotron{
    text-align: center;
  }
  #updateButton{

  }
</style>
