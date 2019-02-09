<template>
  <nav class="navbar navbar-light bg-light">
    <link 
      rel="stylesheet" 
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css" 
      integrity="sha384-GJzZqFGwb1QTTN6wy59ffF1BuGJpLSa9DkKMp0DgiMDm4iYMj70gZWKYbI706tWS" 
      crossorigin="anonymous">
    <a 
      class="navbar-brand" 
      href="/"> Путевка в жизнь </a>
    <ul class="nav">
      <li class="nav-item">
        <a 
          class="nav-link" 
          href="/specialities/"> Специальности </a>
      </li>
      <li class="nav-item">
        <a 
          class="nav-link" 
          href="/universities/"> Вузы </a>
      </li>
    </ul>
    <ul
      v-for="item in items"
      :key="item"
      class="nav">
      <li class="nav-item"> 
        <a 
          :href="'../' + item.slug"
          class="nav-link"> {{ item.Название }} </a>
      </li>
    </ul>
  </nav>
</template>

<script>
import axios from 'axios'
export default {
  data: function() {
    return {
      items: []
    }
  },

  mounted: async function() {
    const response = await axios.get('http://185.158.153.91:1380/pages')
    this.items = response.data
  }
}
</script>
