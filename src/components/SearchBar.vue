<!-- Questo componente sarà la barra di ricerca delle repository di GitHub -->

<!-- Qui va la logica del componente (Vue3 + Javascript) -->
<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      query: '',
      searchType: 'repositories',
    };
  },
  methods: {
    onSearch() {
      this.$emit('search', {
        query: this.query,
        searchType: this.searchType,
      });
    },
  },
};
</script>



<!-- Qui va il contenuto di questo elemento (HTML) -->
<template>
    <div class="search-bar">
      <input
        type="text"
        v-model="query"
        placeholder="Cerca su GitHub..."
      />
      <select v-model="searchType">
        <option value="repositories">Repository</option>
        <option value="users">Utenti/Organizzazioni</option>
      </select>
      <button @click="onSearch">Cerca</button>
    </div>
</template>
  
  



<!-- Qui va lo stile CSS di questo elemento (CSS) -->
<style scoped>
.search-bar {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.search-bar input {
  width: 300px;
  padding: 8px;
  margin-right: 10px;
}

.search-bar button {
  padding: 8px 16px;
}
</style>