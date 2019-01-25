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
    <div class="contacts">
      <h3> Контакты </h3>
      <div style="float: left; width: 200px; height: 200px;">
        <h4> Электронная почта</h4>
        {{ mail }}
      </div>
      <div style="float: left; width: 200px; height: 200px;">
        <h4> Телефон</h4>
        {{ phone }}
      </div>
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
      mail: response.data.Email,
      phone: response.data.Телефон,
      specialities: response.data.специальность
    }
  }
}
</script>

<style>
.contacts {
  margin: 20% 0% 15%;
}
</style>
