<template>
  <div>
    <topmenu />
    <div v-if="pageFound">
      <h4> {{ page.Название }} </h4>
      <h4> {{ page.Текст }} </h4>
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
import Topmenu from '~/components/Topmenu.vue'
import Downfooter from '~/components/Downfooter.vue'
export default {
  components: {
    Topmenu,
    Downfooter
  },
  asyncData: async function({ $axios, params }) {
    const response = await $axios.get('http://185.158.153.91:1380/pages', {
      params: {
        slug: params.slug
      }
    })
    if (response.data.length > 0) {
      return {
        pageFound: true,
        page: response.data[0]
      }
    }
  }
}
</script>
