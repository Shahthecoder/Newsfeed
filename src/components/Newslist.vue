<template>
  <div class="newslist">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img class="media-object" v-bind:src="article.urlToImage">
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">{{ article.title }}</a>
            </h4>
            <h5><em>by {{ article.author }}</em></h5>
            <p>{{ article.description }}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'newslist',
  props: ['source'],
  data() {
    return {
      articles: []
    }
  },
  methods: {
    updateSource: function(source) {
      this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=3164113e36b94e07bd79263e41dd81c1')
      .then(response => {
        this.articles = response.data.articles;
      });
    }
  },
  created: function() {
    this.updateSource(this.source);
  },
  watch: {
    source: function(val) {
      this.updateSource(val);
    }
  }
}
</script>

<style scoped>
  .container {
    font-family: 'Roboto', sans-serif;
  }
  .media-object {
    width: 150px;
    padding: 5px;
  }
  .media {
    border-top: 1px solid lightgrey;
    padding-top: 20px;
  }
</style>
