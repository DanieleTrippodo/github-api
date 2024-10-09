<!-- per visualizzare la lista dei contenuti -->

<!-- Qui va la logica del componente (Vue3 + Javascript) -->
<script>
export default {
  name: 'ResultsList',
  props: {
    results: {
      type: Array,
      required: true,
    },
  },
};
</script>



<!-- Qui va il contenuto di questo elemento (HTML) -->
<template>
  <div class="results-list">
    <div v-for="item in results" :key="item.id" class="result-item">
      <h3>{{ item.full_name }}</h3>
      <p>{{ item.description }}</p>
      <a :href="item.html_url" target="_blank">Vai al repository</a>
    </div>
  </div>
</template>
  



<!-- Qui va lo stile CSS di questo elemento (CSS) -->
<style scoped>
.results-list {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.result-item {
  width: 100%;
  border: 1px solid #ccc;
  padding: 2rem;
  margin-bottom: 16px;
  text-align: left;
}

.result-item h3 {
  margin-top: 0;
  text-decoration: double;
}

.result-item p {
  margin: 8px 0;
}
</style>