<template>
    <div class="container">
      <div class="d-flex flex-column min-vh-100" :class="{ 'justify-content-center':isStartUp }">
        <div class="container-fluid search-bg" :class="{ 'mt-5': !isStartUp}">
          <SearchForm @search="runSearch"></SearchForm>
        </div>
        <div class="container">
          <div class="mt-2">
            <h5 v-if="this.searchQueryStr">Поиск: '{{ searchQueryStr }}'</h5>
            <h6 v-if="searchCompleted">Найдено результатов: {{ searchResults.length }}</h6>
          </div>
          <div class="mt-2">
            <SearchResultList :items="this.searchResults"></SearchResultList>
          </div>
        </div>
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
  computed: {
    isStartUp: function() {
      return !this.searchQueryStr;
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
.search-bg {
  border-radius: 6px;
  padding: 5pt;
  background-color: #2c3e50;
}
</style>
