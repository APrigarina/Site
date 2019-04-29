<template>
  <div>
    <topmenu />
    <top />
    <div v-if="pageFound">
      <div id="uni_container">
        <h1 id="uni_name"> {{ name }} </h1>
        <p id="uni_description">
          {{ description }}
        </p>
      </div>
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
    <link 
      href="https://fonts.googleapis.com/css?family=Montserrat|Roboto+Slab" 
      rel="stylesheet">
  </div>
</template>

<script>
import axios from 'axios'
import Topmenu from '~/components/Topmenu.vue'
import Top from '~/components/Top.vue'
import Downfooter from '~/components/Downfooter.vue'
export default {
  components: {
    Topmenu,
    Top,
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
#uni_container {
  margin-top: 56px;
  margin-right: 157px;
  margin-left: 77px;
}
#uni_name {
  font-family: Roboto Slab;
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  line-height: normal;
  text-transform: uppercase;

  color: #1d262d;
}
#uni_description {
  font-family: Montserrat;
  font-style: normal;
  font-weight: normal;
  font-size: 15px;
  line-height: 29px;

  color: #1d262d;
}
.contacts {
  margin: 20% 0% 15%;
}
</style>
