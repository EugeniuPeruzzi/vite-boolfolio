<script>
import axios from 'axios';


export default {
    name: 'AppMain',
    data() {
        return {
            baseUrl: 'http://localhost:8000',
            posts: []
        }
    },

    created() {
        this.getData();
    },

    methods: {
        getData() {
            // chiamata axios che usa la base url con aggiunta della parte final della chiamata api
            axios.get(`${this.baseUrl}/api/posts`).then((response) => {
                if (response.data.success) {
                    this.posts = response.data.results;
                }
            });
        }
    }

}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <h1 class="text-center">BOOLFOLIO</h1>
            </div>
        </div>
    </div>
    <div class="container">
        <div class="row">
            <div class="col-12 col-md-4" v-for="post in  posts " :key="post.id">
                <div class="card my-3 min-height-200px">
                    <div class="card-image-top">
                        <img :src="`${baseUrl}/storage/${post.image}`" class="img-fluid">
                    </div>
                    <div class="card-body">
                        <div class="card-title">
                            <h2>{{ post.title }}</h2>
                        </div>
                        <p>
                            <span v-if="post.category"><strong>{{ post.category.name }}</strong></span>
                            <span v-else><strong>Tipo non assegnato</strong></span>
                        </p>
                        <p v-if="post.technologies">
                            <span class="badge text-bg-primary me-2" v-for=" technology  in  post.technologies "
                                :key="technology.id">
                                {{ technology.name }}
                            </span>
                        </p>
                        <p>{{ post.content }}</p>
                    </div>
                    <div class="card-footer">
                        <a href="#" class="btn btn-sm btn-primary"> Leggi il progetto</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<style lang="scss"></style>
