<template>
  <div >
  <header class="container">
    <div class="header_content">
      <a href="index.html" class="header_logo" >
        MovieApp</a>
        <button class="top250"
                @click="getMovies(api_url_popular)">
          Top 20
        </button>
      <form @submit.prevent="formSubmitting()">
        <input type="text" class="header_search" placeholder="Search" v-model="search">
      </form>
    </div>
  </header>
  <div class="container">
    <div class="movies" >

      <div class="movie" 
            v-for="movie,i in movies_data"
           :key="movie"
            @click="showModal(movie)">  

        <div class="movie_cover_outer">
          <img :src="movie ? movie.posterUrl : './assets/mortalCombat.jpeg'" class="movie_cover">
          <div class="movie_cover" 
              :class="{darkened: mod == false}"></div>
        </div>
        <div class="movie_info">
          <div class="movie_title">
            {{movie ? movie.nameRu : movies_data}}
          </div>
          <div class="movie_category"
               v-for="genre, i in movie.genres">
            {{movie && i == 0 ? genre.genre 
            : movie && i !== 0 ?  ', ' + genre.genre
            : movies_data}}
          </div>
          <div class="movie_average green"
               :class="{hidden: movie.rating == 'null' || movie.rating == null,
                        green: +movie.rating >= 7.5 ,
                        orange: +movie.rating < 7.5 ,
                        red: +movie.rating < 5.5 }">
            {{movie.rating && movie.rating.includes('%') ? movie.rating.slice(1,-2) 
            : movie.rating && !movie.rating.includes('%') ? movie.rating
            : movie.rating}}
          </div>
        </div>

      </div>

      <div id="myDiv" ref="myDiv" class="modal hidden">
        <MovieCard v-bind:movie="movie"
                   v-bind:hideModal="hideModal"
                   v-bind:pageYOffset="pageYOffset"/>
      </div>

    </div>
  </div>
</div>  
</template>

<script>
import MovieCard from './components/MovieCard.vue'

export default {
  name: 'App',
  data() {
    return {
      movies_data: '',
      movie: '',
      search: '',
      i: 0,
      mod: false,
      vals_arr: [],
      //api_key: "ae74c47c-ab4d-4356-b9d4-7854d005f438",
      api_key: "7f8eaed4-e015-4bf4-ad1d-9c4456c3769b",
      api_url_search: "https://kinopoiskapiunofficial.tech/api/v2.1/films/search-by-keyword?keyword=",
      api_url_popular: "https://kinopoiskapiunofficial.tech/api/v2.2/films/top?type=TOP_100_POPULAR_FILMS&page=1",
    }
  },
  components: {
    MovieCard
  },
  methods: {
  async showMovies(data) {
        this.movies_data = await data.films
        console.log(data.films);
        this.i++
    },
    getMovies(url) {
        fetch(url, {
            headers: {
                "Content-Type": "application/json",
                "X-API-KEY": this.api_key,
            }
        })
        .then(resp => resp.json())
        .then(respData => this.showMovies(respData))
    },
    setRandomRating(rating) {
      rating = (3+Math.random()*5).toFixed(1)
    },
    formSubmitting() {
        const apiSearchUrl = `${this.api_url_search}${this.search}`
        if (this.search !== '') {
            this.getMovies(apiSearchUrl)

            this.search = ''
        }
    },
    showModal(movie) {
      this.$refs.myDiv.classList.remove('hidden')
      this.mod = true
      this.movie = movie

      console.log('modal open');
    }, 
    hideModal(movie) {
      this.$refs.myDiv.classList.add('hidden')
      this.mod = false
      this.movie = movie

      console.log('modal close');
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
        font-weight: 100;
        font-size: 29px;
        position: relative;
        background: transparent;
        border: 1px solid aliceblue;
        border-radius: 2px;
        color: aliceblue;
        opacity: 0.6;
        padding: 0 15px;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.header_content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px;
  height: 60px;
}

.header_logo {
  font-size: 32px;
  text-decoration: none;
  color: #fff;
}

.header_search {
  padding: 8px;
  border: 2px solid #1a191f;
  border-radius: 5px;
  outline: none;
}

.movies {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.movie {
  width: 240px;
  margin: 10px;
  position: relative;
}

.movie_cover_outer {
  width: 200px;
  max-height: 360px;
  position: relative;
}

.movie_cover {
  width: 100%;
  height: 100%;
}

.darkened {
  background-color: #000;
  opacity: 0.1;
  position: absolute;
  top: 0px;
  left: 0;
  right: 0;
  height: 98%;
  z-index: 1;
}

.darkened:hover {
  background-color: grey;
  cursor: pointer;
}

.movie_info {
  padding: 10px 0;
}

.movie_title {
  font-size: 16px;
  color: #fff;
}

.movie_category {
  font-size: 14px;
  color: #ffd80e;
  display: inline-flex;
}

.movie_average {
  position: absolute;
  top: 10px;
  left: 10px;
  right: 0;
  border-radius: 50%;
  width: 36px;
  height: 36px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #1a191f;
  color: #fff;
  font-size: 14px;
}

.green {
  border: 2px solid green;
}

.orange {
  border: 2px solid rgb(251, 226, 0);
}

.red {
  border: 2px solid red;
}

.hidden {
  display: none;
}

.modal {
  width: 100%;
  height: 100%;
  position: absolute;
  top: -100px;
  z-index: 1;
}
</style>


