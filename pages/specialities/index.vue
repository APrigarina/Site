<template>
  <div>
    <topmenu />
    <h1 class="title">
      Специальности
    </h1>
    <h2 class="subtitle">
      Основные специальности
    </h2>
    <ul 
      v-for="speciality in top10"
      :key="speciality">
      <li> 
        <a :href="speciality.id"> {{ speciality.Название }} </a>
      </li>
    </ul>
    <button @click="counter -= 3">Назад</button>
    <button @click="counter += 3">Вперед</button>
    <footer>
      <Downfooter />
    </footer>
  </div>
</template>

<script>
import Topmenu from '~/components/Topmenu.vue'
import Downfooter from '~/components/Downfooter.vue'
export default {
  components: {
    Topmenu,
    Downfooter
  },
  data: function() {
    return {
      counter: 0
    }
  },
  asyncData: async function({ $axios }) {
    const response = await $axios.get('http://185.158.153.91:1380/specialities')
    return {
      specialities: response.data
    }
  },
  computed: {
    top10() {
      return this.specialities.slice(this.counter, this.counter + 3)
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
