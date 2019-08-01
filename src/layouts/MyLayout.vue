<template>
  <q-layout view="hHh lpR fFf">

    <q-header elevated class="bg-primary text-secondary no-shadow">
      <q-toolbar>
        <q-btn round dense flat @click="back" class="absolute">
          <i class="material-icons" v-if="!isHome">
            arrow_back_ios
          </i>
        </q-btn>

        <q-toolbar-title class="text-center text-17">
          {{title}}
        </q-toolbar-title>

        <!--<q-btn class="text-secondary" dense flat round icon="more_horiz" @click="right = !right" />-->
      </q-toolbar>
    </q-header>

    <q-drawer v-model="left" side="left" bordered>
      <!-- drawer content -->
    </q-drawer>

    <q-drawer v-model="right" side="right" bordered>
      <!-- drawer content -->
    </q-drawer>

    <q-page-container>
      <router-view class="p-b-50" />
      <q-page-sticky position="bottom" :offset="[0, 0]">
        <div class="cur-play flex items-center justify-center" @click="openDialog">
          <q-linear-progress rounded :value="0.4" class="q-mt-md cur-play-bar" color="deep-orange-5" track-color="deep-orange-3" />
          <p class="m-b-0">Oh My!<small class="text-l-gray">&nbsp;&nbsp;SEVENTEEN - You Make My Day</small></p>
          <q-btn flat round class="btn text-center btn-cur-play"><img src="~/assets/play-button.svg"></q-btn>
        </div>
      </q-page-sticky>
      <div>
        <q-dialog v-model="adDialog" seamless position="bottom" content-class="ad-block">
          <q-card style="width: 350px">
            <q-card-section class="flex justify-end p-b-0">
              <q-btn dense round flat v-close-popup class="bg-white text-red">
                <i class="material-icons text-24">
                  close
                </i>
              </q-btn>
            </q-card-section>
            <q-card-section class="column items-center no-wrap">
              <div class="text-white text-28 text-center">
                “ Without music,<br> life is a mistake. ”
              </div>
              <p class="text-white text-20 m-t-30">Let’s make it right !</p>
              <div>
                <div class="tab-category tab-blue m-w-165">Subscribe</div>
              </div>
            </q-card-section>
          </q-card>
        </q-dialog>
      </div>
    </q-page-container>

    <q-footer elevated class="text-secondary footer">
      <div class="footer-tabs flex items-center justify-around">
        <q-btn flat round class="btn" to="/"><img src="~/assets/btn_home.svg"></q-btn>
        <q-btn flat round class="btn"><img src="~/assets/btn_search.svg"></q-btn>
        <q-btn flat round class="btn btn-notice"><img src="~/assets/btn_playlist.svg"></q-btn>
      </div>
    </q-footer>

    <!-- dialog -->
    <q-dialog
            v-model="dialog"
            persistent
            :maximized="true"
            transition-show="slide-left"
            transition-hide="slide-right"
    >
      <q-card class="bg-primary cur-music-modal">
        <q-toolbar class="relative">
          <q-btn dense flat v-close-popup class="absolute">
            <i class="material-icons">
              arrow_back_ios
            </i>
          </q-btn>
          <q-btn dense flat round icon="more_horiz" class="absolute r-10" @click="infoDialog = true"/>
          <q-toolbar-title class="text-center text-17">
            Playing Now
          </q-toolbar-title>
        </q-toolbar>

        <q-card-section class="text-center">
          <div class="img-cur-music">
            <q-avatar size="220px">
              <img :src="item.img">
            </q-avatar>
          </div>
          <div>
            <div>
              <div class="text-18">{{item.title}}</div>
              <div class="text-14 text-l-gray">{{item.singer}}</div>
            </div>
          </div>
          <div class="flex m-t-20">
            <div class="col-auto time-block text-10 text-l-gray">03:00</div>
            <div class="col">
              <q-linear-progress rounded :value="0.4" class="q-mt-md" color="deep-orange-5" track-color="white" />
            </div>
            <div class="col-auto time-block text-10 text-l-gray">03:15</div>
          </div>
          <div class="flex items-center justify-around m-t-20">
            <q-btn flat round class="btn text-center"><img src="~/assets/btn_cycle.svg"></q-btn>
            <q-btn flat round class="btn text-center"><img src="~/assets/btn_last-track.svg"></q-btn>
            <q-btn flat round class="btn text-center btn-play"><img src="~/assets/play-button-red.svg"></q-btn>
            <q-btn flat round class="btn text-center"><img src="~/assets/btn_next-track.svg"></q-btn>
            <q-btn flat round class="btn text-center"><img src="~/assets/btn_random.svg"></q-btn>
          </div>
        </q-card-section>
      </q-card>
    </q-dialog>
    <q-dialog
            v-model="infoDialog"
            persistent
            :maximized="true"
            transition-show="slide-left"
            transition-hide="slide-right"
    >
      <q-card class="bg-primary cur-music-modal">
        <q-toolbar class="relative">
          <q-btn dense flat v-close-popup class="absolute">
            <i class="material-icons">
              arrow_back_ios
            </i>
          </q-btn>
          <q-toolbar-title class="text-center text-17">
            Oh My!
          </q-toolbar-title>
        </q-toolbar>
        <q-card-section class="absolute p-x-0">
          <div class="img-cur-music img-helf">
            <q-avatar size="220px">
              <img :src="item.img">
            </q-avatar>
          </div>
        </q-card-section>
        <q-card-section class="text-center m-t-150 p-l-110">
          <div class="info-title-block">
            <div>
              <div class="text-18">{{item.title}}</div>
              <div class="text-14 text-l-gray">{{item.singer}} - {{item.album}}</div>
            </div>
          </div>
        </q-card-section>
        <q-card-section class="m-t-150 flex">
          <div class="flex m-t-20 column">
            <q-list padding class="text-left rounded-borders">
              <q-item clickable v-ripple>
                <q-item-section avatar>
                  <img src="~/assets/subtitles.svg">
                </q-item-section>
                <q-item-section>
                  Lyrics
                </q-item-section>
              </q-item>
              <q-item clickable v-ripple>
                <q-item-section avatar>
                  <img src="~/assets/add-circular-outlined-button.svg">
                </q-item-section>
                <q-item-section>
                  Add to my playlist
                </q-item-section>
              </q-item>
              <q-item clickable v-ripple>
                <q-item-section avatar>
                  <img src="~/assets/share.svg">
                </q-item-section>
                <q-item-section>
                  Share
                </q-item-section>
              </q-item>
            </q-list>
          </div>
        </q-card-section>
      </q-card>
    </q-dialog>
  </q-layout>
</template>

<script>
export default {
  data () {
    return {
      left: false,
      right: false,
      dialog: false,
      infoDialog: false,
      adDialog: true,
      item: { title: 'Oh My!', times: '3:15', singer: 'SEVENTEEN', img: 'https://ppt.cc/fls0Ex@.jpg', album: 'You Make My Day' }
    }
  },
  computed: {
    title () {
      const rName = this.$route.name
      if (rName === 'album') return 'You Make My Day'
      return 'My Favorite'
    },
    isHome () {
      if (this.$route.path === '/') return true
      return false
    }
  },
  methods: {
    openDialog () {
      this.dialog = true
      console.log(this.dialog)
    },
    back () {
      this.$router.go(-1)
    }
  }
}
</script>
