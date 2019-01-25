<template>
  <div>
    <h1> {{ name }} </h1>
    <h4> Описание: </h4>
    {{ description }}
    <h4> Специальности: </h4>
    <ul 
      v-for="speciality in specialities"
      :key="speciality">
      <li >
        <a :href="'/specialities/' + speciality.id"> {{ speciality.Название }} </a>
      </li>
    </ul> 
    <div>
      <h4> Электронная почта</h4>
      {{ mail }}
      <h4> Телефон</h4>
      {{ phone }}
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  asyncData: async function(data) {
    const response = await axios.get(
      'http://185.158.153.91:1380/universities/' + data.params.id
    )
    return {
      name: response.data.Название,
      description: response.data.Описание,
      mail: response.data["Электронная почта"],
      phone: response.data.Телефон,
      specialities: response.data.специальность
    }
  }
}
</script>
