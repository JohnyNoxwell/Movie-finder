<template>
  <div class="home">
    <HelloWorld msg="MovieFinder" />
    <input v-model="search" type="text" class="search" @keyup.enter="searchFilm" />
    <button @click="searchFilm">Search</button>
    <h2 v-if="noResults" class="result-alert">NO RESULTS</h2>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld
  },
  data() {
    return {
      search: "",
      searching: false,
      results: null,
      noResults: false
    };
  },

  methods: {
    searchFilm: function() {
      this.searching = true;
      fetch(`http://www.omdbapi.com/?apikey=e082a6c9&s=${this.search}`)
        .then(res => res.json())
        .then(res => {
          if (res.Response == "False") {
            this.noResults = true;
            console.log(this.noResults);
          } else {
            this.searching = false;
            this.results = res.results;
            this.$router.push({
              name: "Results",
              params: {
                items: res.Search
              }
            });
          }

          console.log(res.Response);
        });
    }
  }
};
</script>
<style>
.home {
  padding-top: 20vh;
}
.search {
  padding: 10px;
  margin-right: 10px;
  /* height: auto; */
  width: 600px;
  font-size: 18px;
}
.result-alert {
  color: rebeccapurple;
}
button {
  padding: 10px;
  font-size: 19px;
  background: #eee;
}
</style>
