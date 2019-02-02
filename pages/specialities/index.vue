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
      v-for="speciality in specialities"
      :key="speciality">
      <li> 
        <a :href="speciality.id"> {{ speciality.Название }} </a>
      </li>
    </ul>
  </div>
</template>

<script>
import Topmenu from '~/components/Topmenu.vue'
export default {
  components: {
    Topmenu
  },
  asyncData: async function({ $axios }) {
    const response = await $axios.get('http://185.158.153.91:1380/specialities')
    return {
      specialities: response.data
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
