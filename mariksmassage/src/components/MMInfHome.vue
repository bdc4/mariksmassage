<template>
  <div style="height: 100vh; overflow: auto;" id="scroll-target" v-scroll:#scroll-target="onScroll">
    <VideoBackground src="src/assets/videos/main.mp4" style="height: 100vh; position: absolute;" class="hidden-xs">
    </VideoBackground>
    <v-img v-for="imgSrc in images" :key="imgSrc" :src="`${imageRoot + imgSrc}`" width="100vw"
      :class="`${(sectionIDs[imgSrc] && sectionIDs[imgSrc].join(' ')) || ''}`">
      <v-container class="h-100 d-flex align-end justify-center">
        <!--v-btn size="x-large">hello</v-btn-->
      </v-container>
    </v-img>
    <div class="mm-button-actions-fixed">
      <v-expand-x-transition>
        <div>
          <div class="d-flex flex-column align-end">
            <v-btn @mouseover="buttonHoverStates[0] = true" @mouseleave="buttonHoverStates[0] = false"
            height="50" :icon="!!shouldShrink(0)" :width="shouldShrink(0) ? undefined : btnWidth" :class="{ 'justify-start': !shouldShrink(0) }">
              <v-icon icon="mdi-calendar" color="success"></v-icon>
              <v-expand-x-transition>
                <span v-show="!shouldShrink(0)" class="ml-2"
                  :style="{ visibility: shouldShrink(0) ? 'hidden' : undefined }">Book Appointment</span>
              </v-expand-x-transition>
            </v-btn>

            <v-btn 
            @mouseover="buttonHoverStates[1] = true" @mouseleave="buttonHoverStates[1] = false"
            :icon="!!shouldShrink(1)" class="mt-2" :class="{ 'justify-start': !shouldShrink(1) }"
              :width="shouldShrink(1) ? undefined : btnWidth" height="50">
              <template v-slot:prepend>
                <div class="d-flex ml-1">
                  <v-icon color="primary">mdi-square-outline</v-icon>
                  <v-icon color="primary" style="position: absolute;">mdi-square-medium</v-icon>
                </div>
              </template>
              <template v-slot:default>
                <template v-if="shouldShrink(1)">
                  <div class="d-flex">
                    <v-icon color="primary" icon="mdi-square-outline"></v-icon>
                    <v-icon color="primary" style="position: absolute;">mdi-square-medium</v-icon>
                  </div>
                </template>

                <v-expand-x-transition>
                  <span v-show="!shouldShrink(1)"
                    :style="{ visibility: shouldShrink(1) ? 'hidden' : undefined }">Pay with Square</span>
                </v-expand-x-transition>
              </template>

            </v-btn>

            <!-- INSTAGRAM -->
            <v-btn @mouseover="buttonHoverStates[2] = true" @mouseleave="buttonHoverStates[2] = false"
            href="https://www.instagram.com/mariksmassage/" target="_blank"
            :icon="!!shouldShrink(2)" :width="shouldShrink(2) ? undefined : btnWidth" height="50"
              class="mt-2" :class="{ 'justify-start': !shouldShrink(2) }">
              <v-icon icon="mdi-instagram" color="rgb(172, 43, 172)"></v-icon>
              <v-expand-x-transition>
                <span v-show="!shouldShrink(2)" class="ml-2"
                  :style="{ visibility: shouldShrink(2) ? 'hidden' : undefined }">View on Instagram</span>
              </v-expand-x-transition>
            </v-btn>

          </div>
        </div>
      </v-expand-x-transition>
    </div>
  </div>
</template>

<script setup>
import VideoBackground from 'vue-responsive-video-background-player'
import { ref } from 'vue';

const offsetTop = ref(0);
const scrollBreakPoint = 50;
const showSmallerButtons = ref(false);
const btnWidth = '220';
var buttonHoverStates = ref([false, false, false]);

const showAlert = () => {
  alert('got it')
}

const onScroll = (e) => {
  offsetTop.value = e.target.scrollTop;
  showSmallerButtons.value = (e.target.scrollTop >= scrollBreakPoint);
}

const shouldShrink = (ind) => {
  return !!showSmallerButtons.value && !buttonHoverStates.value[ind];
}

const imageRoot = 'src/assets/images/';
const images = [
  'pricelist/prices1.jpg', 'specials/special1.jpg', 'specials/special2.jpg'
];
const sectionIDs = {
  'pricelist/prices1.jpg': ['mm-section-0', 'mm-section-1'],
  'specials/special1.jpg': ['mm-section-2']
}
</script>

<style scoped>
.mm-button-actions-fixed {
  position: fixed;
  bottom: 15vh;
  right: calc(max(5vw, 20px));
}
</style>