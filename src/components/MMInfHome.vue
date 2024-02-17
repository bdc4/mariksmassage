<template>
  <div style="height: 100vh; overflow: auto;" id="scroll-target" v-scroll:#scroll-target="onScroll">
    <div class="mm-button-actions-fixed" :style="`${(showSmallerButtons ? 'top: 40vh;' : 'bottom: 100px;')}`">
      <v-expand-x-transition>
        <div>
          <div class="d-flex flex-column align-end" :class="{ 'mm-button-faded': allShouldShrink() }">
            <div :class="{ 'mm-menu-backdrop': (!allShouldShrink() && showButtons) }" id="mmMenuBackdropScrollTarget"
            @click="showButtons = false"
              ></div>
            <v-icon class="toggleUpDown ma-3 hidden-md-and-up" v-show="showSmallerButtons"
              :class='{ "rotate": showButtons }' outlined icon="mdi-arrow-left"
              @click="showButtons = !showButtons"></v-icon>

              <!-- SCHEDULE ON INSTAGRAM BUTTON -->
            <v-btn @mouseover="buttonHoverStates[0] = true" @mouseleave="buttonHoverStates[0] = false" height="50"
              :icon="!!shouldShrink(0)" :width="shouldShrink(0) ? undefined : btnWidth"
              :class="{ 'justify-start': !shouldShrink(0) }">
              <v-icon icon="mdi-calendar" color="success"></v-icon>
              <v-expand-x-transition>
                <span v-show="!shouldShrink(0)" class="ml-2"
                  :style="{ visibility: shouldShrink(0) ? 'hidden' : undefined }">Book Appointment</span>
              </v-expand-x-transition>
              <v-dialog activator="parent" v-model="bookOnInstagramPopup" width="400">
                <v-card>
                  <v-card-title class="d-flex flex-row justify-space-between">
                    <div>Message me on Instagram!</div><v-icon color="primary" icon="mdi-close"
                      @click="bookOnInstagramPopup = false;"></v-icon>
                  </v-card-title>
                  <v-card-text>
                    <v-row>
                      <v-col cols="12">
                        <v-img src="./../assets/images/mark.jpeg" max-height="350"></v-img>
                      </v-col>
                      <v-col>
                        <p>The best way to schedule a massage is to message me on Instagram. The button below will take
                          you there! (If you aren't already logged in, you'll be asked to log into Instagram.)</p>
                        <v-btn color="rgb(172, 43, 172)" variant="elevated" class="mt-5"
                          href="https://www.instagram.com/direct/t/17846127986945126" target="_blank" block>
                          Schedule via Instagram
                          <v-icon class="ml-2" icon="mdi-instagram"></v-icon>
                        </v-btn>
                        <v-btn color="primary" variant="elevated" class="mt-5" block href="tel:5093684368">
                          Schedule via Phone
                          <v-icon class="ml-2" icon="mdi-phone"></v-icon>
                        </v-btn>
                      </v-col>
                    </v-row>
                  </v-card-text>
                </v-card>
              </v-dialog>
            </v-btn>

            <!-- BOOK WITH SQUARE BUTTON -->
            <v-btn @mouseover="buttonHoverStates[1] = true" @mouseleave="buttonHoverStates[1] = false"
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
                  <span v-show="!shouldShrink(1)" :style="{ visibility: shouldShrink(1) ? 'hidden' : undefined }">Prepay with
                    Square</span>
                </v-expand-x-transition>

                <v-dialog activator="parent" v-model="openSquarePopup" min-width="400" height="100vh">
                  <v-card>
                    <v-card-title class="d-flex justify-space-between">
                      <span>Prepay for your appointment!</span>
                      <v-icon icon="mdi-close" @click="openSquarePopup = false;" color="primary"></v-icon>
                    </v-card-title>
                    <v-card-text>
                      <MMBookSquare></MMBookSquare>
                    </v-card-text>
                  </v-card>
                  </v-dialog>
              </template>

            </v-btn>

            <!-- INSTAGRAM -->
            <v-btn @mouseover="buttonHoverStates[2] = true" @mouseleave="buttonHoverStates[2] = false"
              href="https://www.instagram.com/mariksmassage/" target="_blank" :icon="!!shouldShrink(2)"
              :width="shouldShrink(2) ? undefined : btnWidth" height="50" class="mt-2"
              :class="{ 'justify-start': !shouldShrink(2) }">
              <v-icon icon="mdi-instagram" color="rgb(172, 43, 172)"></v-icon>
              <v-expand-x-transition>
                <span v-show="!shouldShrink(2)" class="ml-2"
                  :style="{ visibility: shouldShrink(2) ? 'hidden' : undefined }">View on Instagram</span>
              </v-expand-x-transition>
            </v-btn>

            <!-- GET DIRECTIONS -->
            <v-btn @mouseover="buttonHoverStates[3] = true" @mouseleave="buttonHoverStates[3] = false"
              href="https://maps.app.goo.gl/2SeS95LJw48bt71CA/" target="_blank" :icon="!!shouldShrink(3)"
              :width="shouldShrink(3) ? undefined : btnWidth" height="50" class="mt-2"
              :class="{ 'justify-start': !shouldShrink(3) }">
              <v-icon icon="mdi-map" color="info"></v-icon>
              <v-expand-x-transition>
                <span v-show="!shouldShrink(3)" class="ml-2"
                  :style="{ visibility: shouldShrink(3) ? 'hidden' : undefined }">Get Directions</span>
              </v-expand-x-transition>
            </v-btn>

          </div>
        </div>
      </v-expand-x-transition>
    </div>
    <VideoBackground :src="bgVideo" style="height: 100vh; position: absolute;" class="hidden-xs">
    </VideoBackground>
    <v-img v-for="imgSrc in images" :key="imgSrc" :src="`${imageRoot + imgSrc}`" width="100vw"
      :class="`${(sectionIDs[imgSrc] && sectionIDs[imgSrc].join(' ')) || ''}`">
      <v-container class="h-100 d-flex align-end justify-center">
        <!--v-btn size="x-large">hello</v-btn-->
      </v-container>
    </v-img>
  </div>
</template>

<script setup>
import VideoBackground from 'vue-responsive-video-background-player'
import MMBookSquare from './MMBookSquare'
import { ref } from 'vue';
import bgVideo from '../assets/videos/main.mp4'

var bookOnInstagramPopup = ref(false);
var openSquarePopup = ref(false);
const offsetTop = ref(0);
const scrollBreakPoint = 50;
const showSmallerButtons = ref(false);
const btnWidth = '220';
var showButtons = ref(false);
var buttonHoverStates = ref([false, false, false]);
var pastBreakPoint = ref(false)

const showAlert = () => {
  alert('got it')
}

const onScroll = (e) => {
  var oldVal = offsetTop.value;
  offsetTop.value = e.target.scrollTop;
  pastBreakPoint.value = e.target.scrollTop >= scrollBreakPoint;
  showSmallerButtons.value = (showSmallerButtons.value || pastBreakPoint.value);
  showButtons.value = false;
}

const shouldShrink = (ind) => {
  return window.innerWidth < 960 && !!showSmallerButtons.value && !buttonHoverStates.value[ind] && !showButtons.value;
}

const allShouldShrink = () => {
  return shouldShrink(0) && shouldShrink(1) && shouldShrink(2);
}

const imageRoot = './assets/images/';
const images = [
  'pricelist/prices1.jpg', 'specials/special1.jpg', 'specials/special2.jpg'
];
const sectionIDs = {
  'pricelist/prices1.jpg': ['mm-section-0', 'mm-section-1'],
  'specials/special1.jpg': ['mm-section-2']
}

var buttonStyles = () => {
  const showOnTop = allShouldShrink() || (!allShouldShrink() && showButtons.value);
  return {
    //opacity: allShouldShrink() ? '.75' : '1',
    top: showOnTop ? '100px' : undefined,
    bottom: !showOnTop ? '100px' : undefined
  }
};
</script>

<style scoped lang="scss">
.mm-button-actions-fixed {
  position: fixed;
  right: calc(max(5vw, 20px));
  z-index: 1;
}

.mm-button-faded {
  .v-btn {
    opacity: .5;
    position: relative;
    margin-bottom: -6px;
    z-index: -1;
    top: -190px;
  }

  .toggleUpDown {
    opacity: 0;
    margin-bottom: -10px !important;
    height: 190px;
  }
}

.mm-menu-backdrop {
  position: fixed;
  right: 0;
  top: 0;
  width: 100vw;
  height: 100vh;
  background: black;
  opacity: .75;
}

.toggleUpDown {
  transition: transform .3s ease-in-out !important;
}

.toggleUpDown.rotate {
  transform: rotate(180deg);
}
</style>