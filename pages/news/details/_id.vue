<template>
  <div>
    <topmenu />
    <h1 class="title">
      Новости
    </h1>
    <a> {{ news.Название }} </a>
    <p> {{ news.Полно }} </p>
  </div>
</template>

<script>
import Topmenu from '~/components/Topmenu.vue'
let size = 2
export default {
  components: {
    Topmenu
  },
  asyncData: async function({ $axios, params }) {
    const response = await $axios.get(
      `http://185.158.153.91:1380/news?_id=${params.id}`
    )
    return {
      news: response.data[0]
    }
  }
}
</script>


<style>
.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 50px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 30px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
</style>
