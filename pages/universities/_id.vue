<template>
  <div>
    <topmenu />
    <div v-if="pageFound">
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
    <div v-else>
      Страница не найдена
    </div>
    <footer>
      <Downfooter />
    </footer>
  </div>
</template>

<script>
import axios from 'axios'
import Topmenu from '~/components/Topmenu.vue'
import Downfooter from '~/components/Downfooter.vue'
export default {
  components: {
    Topmenu,
    Downfooter
  },
  asyncData: async function(data) {
    try {
      const response = await axios.get(
        'http://185.158.153.91:1380/universities/' + data.params.id
      )
      return {
        pageFound: true,
        name: response.data.Название,
        description: response.data.Описание,
        mail: response.data.Email,
        phone: response.data.Телефон,
        specialities: response.data.специальность
      }
    } catch (err) {
      pageFound: false
    }
  },
  head() {
    return {
      title: 'Университет: ' + this.name + ' - Путевка в жизнь',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.description
        }
      ]
    }
  }
}
</script>

<style>
.contacts {
  margin: 20% 0% 15%;
}
</style>
