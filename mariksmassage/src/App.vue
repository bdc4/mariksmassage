<template>
  <v-app>
    <v-main>
      <v-app-bar>
        <v-app-bar-title class="text-center">
          <span style="font-family: cursive;">Marik's Massage</span>
        </v-app-bar-title>
      </v-app-bar>
      <!--MMMain></MMMain-->
      <MMInfHome></MMInfHome>
      <v-footer app>
        <v-row justify="center" no-gutters>
          <v-btn style="font-family: cursive;" v-for="(link, index) in links" size="sm" :key="link" variant="text" class="ma-2" rounded="xl"
          @click="scrollTo(index)">
            {{ link }}
          </v-btn>
          <v-col class="text-center mt-2 text-body-2" cols="12">
            {{ new Date().getFullYear() }} — <strong>OmniBrew LLC</strong>
          </v-col>
        </v-row>
      </v-footer>
    </v-main>
  </v-app>
</template>

<script setup>
import MMInfHome from './components/MMInfHome.vue';
import MMMain from './components/MMMain.vue';

const links = [
  'prices', 'services', 'specials'
]

const scrollTo = (index) => {
  document.getElementsByClassName('mm-section-' + index)[0].scrollIntoView({behavior: 'smooth', block: 'nearest'})
}
//
</script>
