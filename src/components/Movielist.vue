<template>
<div>
    <div class="movielist">
      
      <div class="movie card" v-for="movie in movies" v-bind:key="movie.id">
          
          <div class="card_poster relative">
               <img :src=" link_to_image_store + movie.poster_path" alt="">
          </div>
         
          <div class="card_content">
              <div class="movie_title blue_hover">
                  {{movie.original_title}}
              </div>
              <div class="release_date mt-10">
                  {{movie.release_date}}
              </div>
              
          </div>
         
      </div>
    </div>
    <!-- <div class="morebutton" @click="loadMore()">
        load more
    </div> -->
</div>
  
</template>

<script>

export default {


    name: 'Movielist',
    props:{
        movies:{
            type:Array,
            required:true
        }
    },
    data() {
        return {
            link_to_image_store : "https://image.tmdb.org/t/p/original/",
        }
    },
    methods:{
        loadMore(){
            this.$emit('load_more');
        }
    }

}
</script>

<style>
    .movielist{
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(200px,1fr));
      grid-gap: 20px;
    }
    .movie{
        /* max-height: 200px; */
        border-radius: 8px;
    }

    .movie img{
        width: 100%;
        border-radius: 8px;
        cursor: pointer;
        
    }

    .card_content{
        padding: 26px 10px 12px 10px;
    }

    .movie_title{
        color: black;
        font-weight: bold;
    }

    .release_date{
        color: rgba(0,0,0,0.6);
    }

    .relative{
        position: relative;
    }
    .rating{
        position: absolute;
        bottom: -14px;
        border-radius: 50%;
        background: black;
        color: white;
        height: 38px;
        width: 38px;
        left: 10px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .morebutton{
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 10px 20px;
        background: cornflowerblue;
        color: white;
        cursor: pointer;
        width: 100px;
        margin: auto;
        margin-top: 30px;
        border-radius: 5px;
    }

</style>