<template>
  <div>
    <h1>My Favorties list</h1>
    <div id="favorites">
      <div class="movies" v-for="(movie) in WildList" :key="movie.id">
        <div class="movie">
          <h2>{{movie.title}}</h2>
          <div class="movieGroup">
          <img :src="movie.path">
          <button @click="Remove(movie)"> Remove </button>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
 name: 'Favorites',
 data: function() {
   return {
     WildList: []
   }
 },
 created() {
   this.favList()
 },
  methods: {
    async favList() {
      try {
        let response = await axios.get("/api/datas");
        this.WildList = response.data;
        //console.log(response.data);
        return true;
      } catch (error) {
        console.log(error);
      }
    },
    async Remove (movie) {
      //this.$root.$data.Favorites.splice(movieIndex, 1);

      try {
        await axios.delete("/api/datas/" + movie._id);
        this.findData = null;
        this.favList();
        return true;
      } catch (error) {
        console.log(error);
      }
    }
  }
}
</script>

<style scoped>
  .movieGroup {
    display: flex;
    flex-direction: column;
  }

  #favorites {
    margin-bottom: 55px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .movie {
    width: 300px;
  }

</style>
