<template>
  <v-container fluid class="pa-0 ma-0 h-100">
    <VideoBackground src="src/assets/videos/main.mp4" class="h-100">

      <v-card outlined color="transparent" class="h-100 pt-5">
        <v-card-title>
          
        </v-card-title>
        <v-card-text>
          <v-row class="h-100 justify-center">
            <v-col style="max-width: 500px;">
              <v-sheet :elevation="10" class="d-flex align-center justify-center pa-2">
                <v-img src="/src/assets/images/mark.jpeg" width="300" position="center"
                class="">
                <div class="d-flex flex-column justify-space-between h-100">
                  <div class="d-flex justify-space-between ma-2 flex-column align-end h-100">
                    <v-sheet :elevation="10" width="200" class="pa-8 w-50" border rounded>
                      <div class="d-flex flex-column justify-space-between h-100">
                        <v-row><h3>Mark Tsebriy, LMT</h3></v-row>
                        <v-row>Licensed Massage Therapist</v-row>
                        <v-row>Office & Mobile Services</v-row>
                        <v-row>Work with PIP</v-row>
                        <!--li>Office Location: 3001 S Mt Vernon St, Spokane, WA 99223</li-->
                      </div>
                    </v-sheet>
                  </div>
                  <v-col class="d-flex flex-column align-end w-100 h-100">
                    <v-btn class="mb-2 ma-0" width="300" color="success" size="large" variant="elevated"
                      prepend-icon="mdi-calendar-check-outline">Schedule
                      Now</v-btn>
                    <v-btn class="mb-2 ma-0" width="300" color="primary" size="large" variant="elevated">
                      <template v-slot:prepend>
                        <v-icon>mdi-square-outline</v-icon>
                        <v-icon style="position: absolute;">mdi-square-medium</v-icon>
                      </template>Pay with Square</v-btn>
                    <v-btn class="ma-0" variant="elevated" width="300" size="large"
                      style="background-color: rgb(172, 43, 172);">
                      <template v-slot:prepend><v-icon>mdi-instagram</v-icon></template>
                      View Instagram</v-btn>
                  </v-col>
                </div>
                </v-img>
              </v-sheet>
            </v-col>

            <!--v-col class="d-md-flex hidden-md-and-down flex-column">
              <v-btn class="mb-2" size="x-large" block variant="outline"
                prepend-icon="mdi-calendar-check-outline">Schedule Now</v-btn>
              <v-btn class="mb-2" size="x-large" block variant="outline">
                <template v-slot:prepend>
                  <v-icon>mdi-square-outline</v-icon>
                  <v-icon style="position: absolute;">mdi-square-medium</v-icon>
                </template>Pay with Square</v-btn>
            </v-col-->
          </v-row>
        </v-card-text>
        <v-card-actions>
        </v-card-actions>
        <!--v-card-actions class="d-md hidden-md-and-down">
          <v-btn variant="elevated" class="ml-2" size="x-large" style="background-color: rgb(172, 43, 172);">
            <template v-slot:prepend><v-icon class="ml-2">mdi-instagram</v-icon></template>
            View Instagram</v-btn>
        </v-card-actions-->
      </v-card>
    </VideoBackground>
  </v-container>
</template>

<script setup>
import VideoBackground from 'vue-responsive-video-background-player'
</script>

<style scoped></style>