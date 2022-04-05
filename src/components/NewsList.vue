<template>
    <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search</label>
            <input type="search" name="search" v-model="searchTerm" id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
            search term here" />
            <button class="btn btn-primary mb-2">Search</button>
        </div>
        <p>You are searching for {{ searchTerm }}</p>
    </form>
    <div class = "card-group">
        <div v-for="article in articles" class="container_view">
            <div class = "grid_view">
                <img class="card-img-top" :src=" article.urlToImage " alt="">
                <div class="card-body">
                    <h4 class="card-title"> {{ article.title }}</h4>
                    <p class="card-text"> {{ article.description }}</p>
                </div>
            </div> 
        </div>  
    </div>

</template>

<script>
export default {
    data() {
        return {
            articles: [],
            searchTerm: ''
        };
    },
    methods: {
        searchNews() {
            let self = this;
            fetch('https://newsapi.org/v2/everything?q='+
            self.searchTerm + '&language=en', {
    headers: {
        'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
    }
})

        .then(function(response) {
            return response.json();
            })
            .then(function(data) {
                console.log(data);
                self.articles = data.articles;
            });
        }
    }

};
</script>
