<!-- Componente per il loader -->


<!-- Qui va la logica del componente (Vue3 + Javascript) -->
<script>
import debounce from 'lodash.debounce';

export default {
  data() {
    return {
      query: '',
      // Altri dati... da finire
    };
  },
  created() {
    this.debouncedSearch = debounce(this.search, 700);
  },
  methods: {
    search() {
      // Logica della ricerca... da finire
    },
    onInput() {
      this.debouncedSearch();
    }
  }
};

</script>



<!-- Qui va il contenuto di questo elemento (HTML) -->
<template>
  <input type="text" v-model="query" @input="onInput" placeholder="Cerca su GitHub..." />
</template>



<!-- Qui va lo stile CSS di questo elemento (CSS) -->
<style scoped>
button {
  font-weight: bold;
}
</style>