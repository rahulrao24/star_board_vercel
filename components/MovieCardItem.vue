<template>
  <div class="my-1 px-1 w-full md:w-1/2 lg:my-4 lg:px-4 lg:w-1/3">
    <article class="bg-white overflow-hidden rounded-lg shadow-lg h-full">
      <nuxt-link :to="'movies/' + id">
        <div
          class="flex bg-cover bg-no-repeat justify-center"
          v-bind:style="'background-image: url('+'https://image.tmdb.org/t/p/w500'+ poster_path +');'"
        >
          <img
            alt="Placeholder"
            class="block h-64 w-64"
            v-bind:src="`https://image.tmdb.org/t/p/w500${poster_path}`"
          />
        </div>

        <header class="flex items-center justify-between leading-tight p-2 md:p-4">
          <h1 class="text-lg">
            <nuxt-link to class="no-underline hover:underline text-black">{{title}}</nuxt-link>
          </h1>
          <p class="text-grey-darker text-sm">{{release_date}}</p>
        </header>
        <main class="flex items-center justify-center p-2 md:p-4">
          <p class="text-gray-700 text-base text-justify line-clamp">{{overview}}</p>
        </main>

        <footer class="flex items-center justify-between leading-none p-2 md:p-4">
          <div class="flex items-center no-underline text-black" href="#">
            <img
              alt="Placeholder"
              class="block rounded-full"
              src="https://www.svgrepo.com/show/13674/star.svg"
              width="25"
              height="25"
            />
            <p class="ml-2 text-sm">
              {{vote_average}}
              <span>({{vote_count}})</span>
            </p>
          </div>
        </footer>
      </nuxt-link>
    </article>
  </div>
</template>

<script>
export default {
  name: "MovieCardItem",
  props: [
    "id",
    "title",
    "overview",
    "vote_average",
    "vote_count",
    "release_date",
    "poster_path"
  ]
};
</script>
<style>
.line-clamp {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>