<template>
  <div class="container my-12 mx-auto px-4 md:px-12">
    <div class="flex justify-center">
          <SearchMovies v-on:search-text="searchText"/>
    </div>
    <div class="flex flex-wrap -mx-1 lg:-mx-4">
        <MovieCardItem
          v-for="movie in movies"
          :key="movie.id"
          :id="movie.id"
          :title="movie.title"
          :overview="movie.overview"
          :vote_average="movie.vote_average"
          :vote_count="movie.vote_count"
          :release_date="movie.release_date"
          :poster_path="movie.poster_path"
        />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MovieCardItem from "../components/MovieCardItem";
import SearchMovies from "../components/SearchMovies";

export default {
  data() {
    return {
      movies: []
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };

    try {
      const res = await axios.get(
        "https://api.themoviedb.org/3/movie/now_playing?api_key=b866f8118bea76c3f7b91b4ae5ad44fe", config
      );
      this.movies = res.data.results;
    } catch (error) {
      console.log(error);
    }
  },
  methods:{
    async searchText(text){
      const config = {
      headers: {
        Accept: "application/json"
      }
    };

    try {
      const res = await axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=b866f8118bea76c3f7b91b4ae5ad44fe&query=${text}`, config
      );
      this.movies = res.data.results;
    } catch (error) {
      console.log(error);
    }
    }
  },
  head() {
    return {
      title: "Home | Welcome to Star-Board",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Top movie listing app."
        }
      ]
    };
  },
  components: {
    MovieCardItem,
    SearchMovies
  }
};
</script>

<style>


</style>
