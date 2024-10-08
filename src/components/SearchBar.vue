<!-- Questo componente sarà la barra di ricerca delle repository di GitHub -->

<!-- Qui va la logica del componente (Vue3 + Javascript) -->
<script>
    export default {
        data() {
            return {
            query: '',
            searchType: 'repositories', // 'repositories' o 'users'
            results: [],
            isLoading: false,
            errorMessage: ''
            };
        },


    /* CONTINUARE DA QUI */
    };



/* Funzioni o Metodi */
methods: {
    async search() {
        if (this.query.trim().length < 3) {
        this.errorMessage = 'Inserisci almeno 3 caratteri.';
        return;
        }

        this.isLoading = true;
        this.errorMessage = '';

        const endpoint = `https://api.github.com/search/${this.searchType}`;
        const params = new URLSearchParams({
        q: this.query,
        sort: 'stars',
        order: 'desc'
        });

        try {
            const response = await fetch(`${endpoint}?${params.toString()}`);
            const data = await response.json();

        if (data.items.length === 0) {
            this.errorMessage = 'Nessun risultato trovato.';
        } else {
            this.results = data.items;
        }
        } catch (error) {
        console.error('Errore:', error);
        this.errorMessage = 'Si è verificato un errore durante la ricerca.';
        } finally {
            this.isLoading = false;
        }
    }
}

</script>



<!-- Qui va il contenuto di questo elemento (HTML) -->
<template>
    <div>
      <input type="text" v-model="query" @input="onInput" placeholder="Cerca su GitHub..." />
      <select v-model="searchType">
        <option value="repositories">Repository</option>
        <option value="users">Utenti/Organizzazioni</option>
      </select>
      <button @click="search">Cerca</button>
      <p v-if="errorMessage">{{ errorMessage }}</p>
    </div>
</template>
  



<!-- Qui va lo stile CSS di questo elemento (CSS) -->
<style scoped>
button {
  font-weight: bold;
}
</style>