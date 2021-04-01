<template>
<div class="Moves">
  <p>Use these buttons to find your favorite movies by the decades and add them to your favorites list.</p>
  <p>Click on <strong>Favorites</strong> above to view your list</p>

<div class="MovieButtons">
<button @click="earlyMovies()"> early 1900s</button>
<button @click="fourties()"> 1940s</button>
<button @click="fifties()"> 1950s</button>
<button @click="sixties()"> 1960s</button>
<button @click="seventies()"> 1970s</button>
<button @click="eighties()"> 1980s</button>
<button @click="nineties()"> 1990s</button>
<button @click="twothousands()"> 2000s</button>
<button @click="twothousandtens()"> 2010+</button>
<button @click="yourMovies()">Your Movies</button>

<div v-if="!(isYourMovies)" id="oldMovies">
<div class="movies" v-for="movie in filteredMovies" :key="movie.id">
<div class="movie">
<button @click="addFavorites(movie)"> Add To Favorites </button>

<div class="groupMovie">
<img :src="movie.image">
<h2>{{movie.fullTitle}}</h2>
</div>
</div>
</div>


</div>

<div v-if="isYourMovies" id="oldMovies">
<div class="movies" v-for="movie in filteredMovies" :key="movie.id">
<div class="movie">
<button @click="addFavorites(movie)"> Add To Favorites </button>
<div class="groupMovie">
<img :src="movie.path">
<h2>{{movie.title}}</h2>

</div>
</div>
</div>


</div>


</div>
</div>


</template>


<script>
import axios from 'axios';

  export default {
 name: 'Find',
 data: function() {
 return {
 filteredMovies: [],
 isYourMovies: false
 }
 },
  methods: {
    earlyMovies () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year < 1940) {
      this.filteredMovies.push(movie[i])
      }

      }
    },
    fourties () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year >= 1940 && movie[i].year < 1950) {
      this.filteredMovies.push(movie[i])
      }

      }
    },
    fifties () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year >= 1950 && movie[i].year < 1960) {
      this.filteredMovies.push(movie[i])
      }

      }

    },
    sixties () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year >= 1960 && movie[i].year < 1970) {
      this.filteredMovies.push(movie[i])
      }

      }

    },
    seventies () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year >= 1970 && movie[i].year < 1980) {
      this.filteredMovies.push(movie[i])
      }

      }

    },
    eighties () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year >= 1980 && movie[i].year < 1990) {
      this.filteredMovies.push(movie[i])
      }

      }

    },
    nineties () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year >= 1990 && movie[i].year < 2000) {
      this.filteredMovies.push(movie[i])
      }

      }

    },
    twothousands () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year >= 2000 && movie[i].year < 2010) {
      this.filteredMovies.push(movie[i])
      }

      }

    },
    twothousandtens () {
      this.isYourMovies = false;
      let movie = this.$root.$data.Movies
    //  console.log(movie)
      this.filteredMovies = []

      for(let i = 0; i < movie.length; ++i) {
      if(movie[i].year >= 2010) {
      this.filteredMovies.push(movie[i])
      }

      }

    },
    async addFavorites (movie) {
     //console.log("helloooo")
     //this.$root.$data.Favorites.push(movie);

     if(this.isYourMovies) {
       try {
         await axios.post('/api/datas', {
           title: movie.title,
           path: movie.path
         });
       } catch (error) {
         console.log(error);
       }
     }
     else {
       try {
         await axios.post('/api/datas', {
           title: movie.fullTitle,
           path: movie.image
         });
       } catch (error) {
         console.log(error);
       }
     }



   },
   async yourMovies() {
     this.isYourMovies = true;
     try {
       let response = await axios.get("/api/movies");
       this.filteredMovies = response.data;
       return true;
     } catch (error) {
       console.log(error);
     }
   }


  },


}


</script>

<style scoped>

  .groupMovie {
    display: flex;
    flex-direction: column;

  }

  #oldMovies {
    margin-bottom: 55px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;

  }

  .movie {
    width: 130px;
  }

  h2 {
    font-size: 15px;
  }

  .movie button {
    margin-top: 5px;
    width: 130px;
  }

</style>
