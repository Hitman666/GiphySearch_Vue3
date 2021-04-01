<template>
    <div class="hello">
        <h1>{{ msg }}</h1>

        <input name="search" v-model="searchTerm" />
        <button @click="performSearch()">Search</button>

        <img v-for="g in giphies" :key="g.id" :src="g.images.fixed_height_small.url" />
    </div>
    <a href="https://developers.giphy.com/docs/api#quick-start-guide">
        <img src="giphy.png" alt="" class="giphyAttribution" />
    </a>
</template>

<script>
import axios from 'axios';

export default {
    name: 'HelloWorld',
    props: {
        msg: String
    },
    data() {
        return {
            searchTerm: 'cats',
            giphies: []
        };
    },
    methods: {
        performSearch() {
            let API_KEY = 'getYourOwn';
            let link = `https://api.giphy.com/v1/gifs/search?api_key=${API_KEY}&limit=5&offset=0&rating=g&lang=en&q=`;
            let apiLink = link + this.searchTerm;

            axios
                .get(apiLink)
                .then((response) => {
                    this.giphies = response.data.data;
                })
                .catch((error) => {
                    console.error(error);
                });
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}
ul {
    list-style-type: none;
    padding: 0;
}
li {
    display: inline-block;
    margin: 0 10px;
}
a {
    color: #42b983;
}

.giphyAttribution {
    margin-top: 30px;
}
</style>
