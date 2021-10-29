<template>
  <div>
    <div v-for="(movie, index) in movies" :key="index">
      <div>
        <img :src="`https://image.tmdb.org/t${movie.poster_path}`" alt="/" />
        <p>{{ movie.vote_average }}</p>
        <p>{{ movie.overview }}</p>
      </div>
      <div>
        <p>
          {{ movie.title.slice(0, 25)
          }}<span v-if="movie.title.length > 25">...</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      movies: [],
    }
  },
  async fetch() {
    await this.getMovies()
  },
  methods: {
    async getMovies() {
      const data = axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=f032274d9c9fd3adb40ade7cdc65485b&language=en-US&page=1&query=$20`
      )
      const result = await data
      result.data.results.forEach((movie) => {
        this.movies.push(movie)
      })
      console.log(result)
    },
  },
}
</script>
