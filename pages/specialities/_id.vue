<template>
  <div>
    <h1> {{ name }} </h1>
    <h4> Описание: </h4>
    {{ description }}
    <h4> ВУЗы: </h4>
    <ul 
      v-for="university in universities"
      :key="university">
      <li >
        <a :href="'/universities/' + university.id"> {{ university.Название }} </a>
      </li>
    </ul> 
  </div>
</template>

<script>
import axios from 'axios'

export default {
  asyncData: async function(data) {
    const response = await axios.get(
      'http://185.158.153.91:1380/specialities/' + data.params.id
    )
    return {
      name: response.data.Название,
      description: response.data.Описание,
      universities: response.data.вузы
    }
  }
}
</script>
