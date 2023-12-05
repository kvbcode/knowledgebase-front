<template>
    <div class="container">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand">Поиск по документам</a>
        <SearchForm @search="runSearch" class="d-flex" type="Search"></SearchForm>
      </div>
    </nav>
      <div class="mt-2">
        <h5 v-if="this.searchQueryStr">Поиск: '{{ searchQueryStr }}'</h5>
        <h6 v-if="searchCompleted">Найдено результатов: {{ searchResults.length }}</h6>
      </div>
      <div class="mt-2">
        <SearchResultList :items="this.searchResults"></SearchResultList>
      </div>
    </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.min.css'
import SearchForm from './components/SearchForm.vue'
import SearchResultList from './components/SearchResultList.vue';

export default {
  name: 'App',
  components: {
    SearchForm, SearchResultList
  },
  data() {
    return {
      searchQueryStr: '',
      searchResults: [],
      searchCompleted: false
    }
  },
  methods: {
    runSearch(ev){
      const url = new URL('http://cyberwork:8080/search');
      url.searchParams.set('q', ev);

      this.searchQueryStr = ev;
      this.searchResults = []
      this.searchCompleted = false;

      fetch(url)
        .then(resp => {
          if (resp.ok) return resp.json();
          console.log(resp);
        })
        .then(json => {
          if (json){
            this.searchCompleted = true;
            console.log('found results: ' + json.length);
            this.searchResults = json;
          }
        });
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.app-content {
  width: 50%;
  margin: auto;
}
</style>
