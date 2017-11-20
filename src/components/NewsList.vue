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
            <button class="accordion">{{article.title}}</button>
            <div class="panel">
              <p>{{article.description}}</p>
              <a v-bind:href="article.url" target="_blank">Read full news</a>
            </div>
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
            this.showDescription();
          }).catch(function () {
            alert("Sorry, we could find news for you. PLease try again later")
            console.log("EXCEPTION");
        })
      },
      showDescription: function(){
       console.log("show");

        var acc = document.getElementsByClassName("accordion");
        var i;
        console.log(acc.length);
        if(acc.length ===0 ) this.updateSource();
        for (i = 0; i < acc.length; i++) {
          acc[i].onclick = function(){
            this.classList.toggle("active");
            var panel = this.nextElementSibling;
            if (panel.style.display === "block") {
              panel.style.display = "none";
            } else {
              panel.style.display = "block";
            }
          }
        }
      }
    },
    created: function(){
      console.log("CREATED");
     this.updateSource();
    }
  }

</script>

<style scoped>

  .jumbotron{
    text-align: center;
  }
  button.accordion {
    background-color: #eee;
    color: #444;
    cursor: pointer;
    padding: 18px;
    width: 100%;
    border: none;
    text-align: left;
    outline: none;
    font-size: 15px;
    transition: 0.4s;
  }
  button.accordion.active, button.accordion:hover {
    background-color: #ccc;
  }

  div.panel {
    padding: 0 18px;
    display: none;
    background-color: white;
  }

</style>
