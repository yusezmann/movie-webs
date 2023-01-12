<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <div class="detail flex flex-row">
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img rounded-md">
    <p><span>Genre: </span>{{ movie.Genre }}</p>
    <p><span>Director: </span>{{ movie.Director }}</p>
    <p><span>Tahun Rilis: </span>{{ movie.Year }}</p>
    <p><span>Rating: </span>{{ movie.imdbRating }}</p>
    </div>
    <h3>Description:</h3>
    <p>{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'
import env from '@/env.js'
export default {
  setup () {
    const movie = ref({})
    const route = useRoute()

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(res => res.json())
        .then(data => {
          movie.value = data
          console.log(data);
        })
    })

    return {
      movie,
      route
    }
  }
}
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;

  h2 {
    color: #FFF;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
    text-align: center;
  }

  .featured-img {
    display: block;
    margin-left: auto;
    margin-right: auto;
    max-width: 200px;
    margin-bottom: 16px;
  }

  p {
    color: #FFF;
    font-size: 18px;
    line-height: 1.4;

    span {
      color: #000;
      font-weight: 600;
    }
  }

}

</style>