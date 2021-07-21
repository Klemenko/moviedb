<template>
    <div>
        <h2>Popularni filmi</h2>
        <div class="home-grid">
            <Sidebar :genres="genres" @filters_updated="filterMovieList($event)" />
            <Movielist :movies="movies_to_show" />
        </div>
    </div>
</template>

<script>
import Sidebar from '../components/Sidebar.vue'
import Movielist from '../components/Movielist.vue'
const axios = require('axios').default;

export default {
    name: 'Home',
    components: {
        Sidebar,
        Movielist
    },
    data() {
        return {
            movies:[],
            genres:[],
            genre_filter_list:[],
        }
    },
    mounted(){
        this.getMovies();
        this.getGenres();
    },
    methods:{

        getMovies(){

            const api_url = "https://api.themoviedb.org/3/movie/popular";
            const params = {
                api_key : '533768cb32183a678781d4bbe84a2493',
                language: 'en-US',
                page: 1
            }

            axios.get(api_url,{
                params
            }).then(response => {
                console.log(response.data);
                 this.movies = response.data.results;
            })
        },
        getGenres(){

            const api_url = "https://api.themoviedb.org/3/genre/movie/list";
            const params = {
                api_key : '533768cb32183a678781d4bbe84a2493',
                language: 'en-US'
            }

            axios.get(api_url,{
                params
            }).then(response => {
                console.log(response.data);
                this.genres = response.data.genres;
            })

        },

        filterMovieList(genre_list){
            this.genre_filter_list = genre_list;
           
        },

    },
    computed:{
        movies_to_show(){
            if(this.genre_filter_list.length < 1){
                return this.movies
            }
            var filtered_movies = this.movies.filter(movie => {
                let intersect_check = this.genre_filter_list.filter(value => movie.genre_ids.includes(value)).length > 0;
                if(intersect_check){
                    return movie;
                }
            });
            return filtered_movies;
        }
    }


}
</script>

<style>



.home-grid{
    display: grid;
    grid-template-columns: 250px 3fr;
    column-gap: 30px;
}
.card{
    box-shadow: 0 2px 8px rgb(0 0 0 / 10%);
    border: 1px solid gainsboro;
    background-color: #fff;
}

@media (max-width: 500px) {
  .home-grid{
       grid-template-columns: 1fr;
  }
}


</style>