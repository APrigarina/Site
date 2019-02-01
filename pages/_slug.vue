<template>
  <div>
    <div v-if="pageFound">
      {{ page }}
    </div>
    <div v-else>
      Страница не найдена
    </div>
  </div>
</template>

<script>
export default {
  asyncData: async function({ $axios, params }) {
    const response = await $axios.get('http://185.158.153.91:1380/pages', {
      params: {
        slug: params.slug
      }
    })

    const pageArr = response.data
    if (response.data.lenght > 0) {
      return {
        pageFound: true,
        page: response.data[0]
      }
    } else {
      return {
        pageFound: false
      }
    }
  }
}
</script>
