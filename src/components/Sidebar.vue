<template>
  <div class="sidebar">
      <div class="card">
          Filter by Genres
        <div class="genres-list">
            <div class="genre" v-for="genre in genres" v-bind:key="genre.id" @click="toggleGenreFilter(genre)" :class="{'active_filter' : genre_filter.includes(genre.id) }">
                {{genre.name}}
            </div>
        </div>
      </div>
      
  </div>
</template>

<script>
export default {
    name: 'Sidebar',
    props:["genres"],
    data: function(){
        return {
             genre_filter:[],
        }
       
    },
    methods:{
        toggleGenreFilter(genre){

            let contains_check = this.genre_filter.find( element => element == genre.id);
            
            if(contains_check){
                this.genre_filter = this.genre_filter.filter(element => element != genre.id);
            }else{
                this.genre_filter = [...this.genre_filter,genre.id];
            }
        }
    },
    watch:{
        genre_filter(newVal){
            this.$emit('filters_updated',newVal);
        }
    }
}
</script>

<style>
    .sidebar{

    }

    .sidebar .card{
        padding: 10px;
    }

    .genre{
        border: 1px solid #9e9e9e;
        border-radius: 14px;
        padding: 4px 12px;
        font-size: 0.9em;
        display: inline-flex;
        margin-right: 6px;
        margin-top: 8px;
    }
    .genre:hover{
        color: white;
        background: rgb(1,180,228);
        cursor: pointer;
    }

    .active_filter{
        background: rgb(1,180,228);
        color: white;
    }

</style>