<template>
  <form @submit.prevent="onSubmit" class="bg-white w-full max-w-sm mb-8 py-2 px-2 rounded-md">
      <div class="flex items-center border-b border-b-2 border-indigo-500 py-2">
      <input type="text" v-model="text" placeholder="Search movies..." class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none">
      <input type="submit" value="Search" class="flex-shrink-0 bg-indigo-500 hover:bg-indigo-700 border-indigo-500 hover:border-indigo-700 text-sm border-4 text-white py-1 px-2 rounded">
  </div>
  </form>
</template>

<script>
export default {
    name: 'SearchMovies',
    data(){
        return {
            text: ''
        }
    },
    methods: {
        onSubmit(){
            this.$emit('search-text', this.text);
            this.text = '';
        }
    }
}
</script>

<style>

</style>