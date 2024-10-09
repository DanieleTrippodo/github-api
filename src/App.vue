<template>
  <div id="app">
    <h1>GitHub Repository Search</h1>
    <SearchBar @search="performSearch" />
    <div v-if="isLoading">Caricamento...</div>
    <div v-else>
      <p v-if="errorMessage">{{ errorMessage }}</p>
      <ResultsList v-else :results="results" />
    </div>
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import ResultsList from './components/ResultsList.vue';

export default {
  name: 'App',
  components: {
    SearchBar,
    ResultsList,
  },
  data() {
    return {
      results: [],
      isLoading: false,
      errorMessage: '',
    };
  },
  methods: {
    async performSearch(query) {
      if (query.trim().length < 3) {
        this.errorMessage = 'Inserisci almeno 3 caratteri per la ricerca.';
        this.results = [];
        return;
      }

      this.isLoading = true;
      this.errorMessage = '';
      this.results = [];

      const endpoint = `https://api.github.com/search/repositories?q=${encodeURIComponent(
        query
      )}`;

      try {
        const response = await fetch(endpoint);
        const data = await response.json();

        if (data.items && data.items.length > 0) {
          this.results = data.items;
        } else {
          this.errorMessage = 'Nessun risultato trovato.';
        }
      } catch (error) {
        console.error('Errore nella ricerca:', error);
        this.errorMessage = 'Si è verificato un errore durante la ricerca.';
      } finally {
        this.isLoading = false;
      }
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  padding: 20px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

h1 {
  margin-bottom: 20px;
}

body{
  background-color: rgb(46, 46, 46);
}
</style>
