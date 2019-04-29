<template>
  <div id="main">
    <topmenu />
    <section class="middle_container">
      <div class="text_container">
        <h1 class="title">
          Путевка в жизнь
        </h1>
        <p id="text"> Разнообразный и богатый опыт говорит нам, 
        что высококачественный прототип будущего проекта способствует 
        повышению качества благоприятных перспектив! 
        Господа, современная методология разработки влечет за собой 
        процесс внедрения и модернизации благоприятных перспектив.
        В целом, конечно, постоянное информационно-пропагандистское
        обеспечение нашей деятельности предопределяет высокую 
        востребованность экономической целесообразности принимаемых решений.
        </p>
      </div>
      <span>
        <img 
          id="picture"
          src="~/static/images/middle/picture.png">
      </span>
    </section>
    <div id="spec_group">
      <ul class="spec_group_text">
        <li 
          v-for="(item, index) in directions" 
          :key="item.Название">
          <a
            @click="activeDir = index"> {{ item.Название }} </a>
        </li>
      </ul>
    </div> 
    <section class="below_middle_container">
      <ul>
        <li 
          v-for="(item, index) in specialities"
          id="list_spec"
          :key="item.Название">
          <a
            class="specialities"
            href="#description"
            @click="activeSpec = index"> {{ item.Название }} </a>
        </li>
      </ul>
      <div class="div_description">
        <div class="description">
          {{ specialities[activeSpec].Описание }}
        </div>
        <a :href="'/specialities/' + specialities[activeSpec].id"> Подробнее </a>
      </div>
    </section>
    <section>
      <p id="column_text">
        Разнообразный и богатый опыт говорит нам, 
        что высококачественный прототип будущего проекта способствует 
        повышению качества благоприятных перспектив! 
        Господа, современная методология разработки влечет за собой 
        процесс внедрения и модернизации благоприятных перспектив.
        В целом, конечно, постоянное информационно-пропагандистское
        обеспечение нашей деятельности предопределяет высокую 
        востребованность экономической целесообразности принимаемых решений.
      </p>
    </section>
    <footer>
      <Downfooter />
    </footer>
    <link 
      href="https://fonts.googleapis.com/css?family=Roboto+Slab|Montserrat" 
      rel="stylesheet">
  </div>
</template>

<script>
import Topmenu from '~/components/Topmenu.vue'
import Downfooter from '~/components/Downfooter.vue'
import constants from '~/assets/constants'
export default {
  components: {
    Topmenu,
    Downfooter
  },
  async asyncData({ $axios }) {
    const responseDir = await $axios.get(constants.baseUrl + '/directions')
    return {
      activeDir: 0, 
      directions: responseDir.data
    }
  },
  async asyncData({ $axios }) {
    const response = await $axios.get(constants.baseUrl + '/specialities')
    return {
      activeSpec: 0,
      specialities: response.data
    }
  },
  head() {
    return {
      title: "Сайт профориентации 'Путевка в жизнь'",
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Сайт профориентации для абитуриентов Нижегородской области'
        }
      ]
    }
  }
}
</script>

<style>
#main {
  margin-left: 117px;
}
.middle_container {
  display: flex;
  align-items: center;
}
.text_container {
  margin-right: 42px;
}
.title {
  width: 476px;
  height: 64px;
  font-family: 'Roboto Slab';
  font-style: normal;
  font-weight: bold;
  line-height: normal;
  font-size: 48px;
  text-transform: uppercase;
  color: #5d3dc6;
  margin-bottom: 43px;
}
#picture {
  width: 600px;
  height: 496px;
}
#text {
  width: 582px;
  height: 235px;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: normal;
  line-height: 29px;
  font-size: 15px;
  color: #1d262d;
}
.below_middle_container {
  display: inline-flex;
}
#spec_group {
  margin-bottom: 40px;
  display: flex;
}
.spec_group_text {
  font-family: 'Roboto Slab', serif;
  font-style: normal;
  font-weight: bold;
  line-height: normal;
  font-size: 20px;
  text-align: center;
  text-transform: uppercase;
  color: #fe5e5d;
  padding-bottom: 6px;
  padding-right: 19px;
  padding-left: 19px;
  border-bottom: 4px solid #fe5e5d;
}
#list_spec {
  z-index: 5;
  left: -37px;
  list-style-type: none;
  position: relative;
}
.specialities {
  display: block;
  width: 366px;
  height: 56px;
  padding: 17px;
  font-family: 'Montserrat';
  font-style: normal;
  font-weight: normal;
  line-height: normal;
  font-size: 18px;
  text-decoration: none;

  color: #41505c;
}
.specialities:focus {
  background-image: url('/images/below_middle/rectangle.png');
  background-size: cover;
  font-weight: bold;
  color: #ffffff;
}
.div_description {
  position: relative;
  left: -52.5px;
  width: 816px;
  background: #ffffff;
  box-shadow: 0px 2px 11px rgba(85, 102, 129, 0.15);
}
.description {
  margin: 33px 64px 70px 73px;

  font-family: Montserrat;
  font-style: normal;
  font-weight: normal;
  line-height: 29px;
  font-size: 15px;

  color: #1d262d;
}
#column_text {
  display: block;
  margin: 93px 117px 0px 0px;

  font-family: Montserrat;
  font-style: normal;
  font-weight: normal;
  line-height: 29px;
  font-size: 15px;

  column-count: 2;
  column-gap: 35px;

  color: #1d262d;
}
</style>
