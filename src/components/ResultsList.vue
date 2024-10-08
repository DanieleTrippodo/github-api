<!-- per visualizzare la lista dei contenuti -->

<!-- Qui va la logica del componente (Vue3 + Javascript) -->
<script>
export default {
  data() {
    return {
      count: 0
    }
  }
}
</script>



<!-- Qui va il contenuto di questo elemento (HTML) -->
<template>
    <div>
      <SearchBar @search="search" />
      <Loader v-if="isLoading" />
      <p v-if="errorMessage">{{ errorMessage }}</p>
      <ResultsList v-else :results="results" :searchType="searchType" />
    </div>
</template>
  



<!-- Qui va lo stile CSS di questo elemento (CSS) -->
<style scoped>
button {
  font-weight: bold;
}
</style>