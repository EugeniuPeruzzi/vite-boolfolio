<script>
import axios from 'axios';


export default {
    data() {
        return {
            baseUrl: 'http://127.0.0.1:8000/',
            loading: true,
        }
    },
    methods: {
        getData() {
            // chiamata axios che usa la base url con aggiunta della parte final della chiamata api
            axios.get(`${baseUrl}/api/posts`).then((response) => {
                if (response.data.success) {
                    this.post = response.data.results;
                    this.loading = false;
                }
            });
        }
    }

}
</script>

<template>
    <h1>ciaoo come va?</h1>
</template>


<style lang="scss"></style>
