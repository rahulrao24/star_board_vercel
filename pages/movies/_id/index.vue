<template>
  <div>
    <section
      style="backgroundImage: url('https://images.unsplash.com/photo-1524985069026-dd778a71c7b4?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=751&q=80')"
      class="h-screen flex justify-center w-full bg-cover bg-no-repeat"
    >
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 w-11/12 items-center justify-center">
        <div class="flex justify-center">
          <div class="w-48">
            <img
              v-bind:src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
              alt
              class="w-full h-64 min-w-full rounded-lg shadow-xl"
            />
          </div>
        </div>
        <div>
          <h2 class="inline text-3xl text-white">{{movie.title}}</h2>
          <p class="text-gray-100">{{movie.tagline}}</p>
          <div class="flex ml-4">
            <img
              alt="Placeholder"
              class="block rounded-full"
              src="https://www.svgrepo.com/show/13674/star.svg"
              width="25"
              height="25"
            />
            <p class="ml-4 text-white my-1">{{movie.vote_average}} ({{movie.vote_count}})</p>
          </div>

          <p class="text-base leading-loose text-gray-400">{{movie.overview}}</p>

          <p class="text-white text-sm font-bold mt-12">
            <GenresTag
              v-for="genre in movie.genres"
              :key="genre.id"
              :id="genre.id"
              :name="genre.name"
            />
            <span>|</span>
            {{movie.release_date}}
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import GenresTag from "../../../components/GenresTag";

export default {
  data() {
    return {
      movie: {}
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
        `https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=b866f8118bea76c3f7b91b4ae5ad44fe`,
        config
      );
      this.movie = res.data;
    } catch (error) {
      console.log(error);
    }
  },
  head() {
    return {
      title: "Movie Details | Welcome to Star-Board",
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
    GenresTag
  }
};
</script>

<style>
span {
  @apply mx-2;
}
</style>