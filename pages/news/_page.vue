<template>
  <div>
    <topmenu />
    <h1 class="title">
      Новости
    </h1>
    <ul 
      v-for="news in allNews"
      :key="news">
      <li> 
        <a :href="'details/' + news.id"> {{ news.Название }} </a>
        <p> {{ news.Кратко }} </p>
      </li>
    </ul>
    <div
      v-for="number in buttonAmount"
      :key="number">
      <div v-if="number==page">
        <button><a :href="'/news/' + number"><b>{{ number }}</b></a></button>
      </div>
      <div v-else>
        <button> <a :href="'/news/' + number"> {{ number }} </a> </button>
      </div>
    </div>
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
    const page = params.page
    const response = await $axios.get(
      `http://185.158.153.91:1380/news?_limit=${size}&_start=${(page - 1) *
        size}`
    )
    const pageAmount = await $axios.get('http://185.158.153.91:1380/news/count')
    var buttonAmount =
      Math.floor(pageAmount.data / size) + (pageAmount.data % size > 0 ? 1 : 0)
    return {
      allNews: response.data,
      buttonAmount
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

button {
  background: white;
  border: white;
}

</style>
