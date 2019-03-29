<template>
  <div>
    <topmenu />
    <div v-if="pageFound">
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
      <h4> Профессии </h4>
      <ul>
        <li 
          v-for="(profession, index) in professions"
          :key="profession">
          <a 
            href="#description"
            @click="activeItem = index"> {{ profession.Название }} </a>
        </li>
      </ul>
      <div>
        <div v-html="professions[activeItem].Видео" />
        <div v-html="$md.render(professions[activeItem].Описание)"/>
      </div>
    </div>
    <div v-else>
      <h4> Страница не найдена</h4>
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
        'http://185.158.153.91:1380/specialities/' + data.params.id
      )
      return {
        pageFound: true,
        name: response.data.Название,
        description: response.data.Описание,
        universities: response.data.вузы,
        professions: response.data.профессии,
        activeItem: 0
      }
    } catch (err) {
      pageFound: false
    }
  }
}
</script>
