<template>
  <q-page class="flex column items-center justify-start p-x-40">
    <div class="w-100-p">
      <q-input class="search-bar m-t-10" rounded outlined v-model="text">
        <template v-slot:append>
          <q-icon name="search" class="text-l-gray" />
        </template>
      </q-input>
    </div>
    <div class="flex w-100-p items-center justify-around m-t-30">
      <div class="tab-category" :class="{'tab-blue': activeList('playlist')}" @click="curList = 'playlist'">Playlist</div>
      <div class="tab-category" :class="{'tab-blue': activeList('album')}" @click="curList = 'album'">Album</div>
      <div class="tab-category" :class="{'tab-blue': activeList('artist')}" @click="curList = 'artist'">Artist</div>
    </div>
    <div class="w-100-p">
      <ul class="music-list">
        <li class="row list-item" v-for="(item, iIndex) in list" :key="iIndex">
          <div class="col-auto l-block">
            <q-avatar size="111px" @click="goAlbum(iIndex)">
              <img :src="item.img">
            </q-avatar>
          </div>
          <div class="col r-block flex column items-start justify-center">
            <div>
              <div class="m-b-5 text-18" @click="goAlbum(iIndex)">{{item.title}}</div>
              <div class="text-12">{{item.num}} songs ‧ {{item.times}} min</div>
            </div>
            <div class="play-panel flex">
              <q-btn flat round class="btn text-center"><img src="~/assets/play-button.svg"></q-btn>
              <q-btn flat round class="btn text-center"><img src="~/assets/btn_cycle.svg"></q-btn>
              <q-btn flat round class="btn text-center"><img src="~/assets/btn_random.svg"></q-btn>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      searchModel: '',
      curList: 'playlist',
      text: '',
      list: [
        { title: 'You Make My Day', num: 6, times: 19, img: 'https://ppt.cc/fls0Ex@.jpg' },
        { title: '9-TEEN', num: 1, times: 3, img: 'https://ppt.cc/ffMWXx@.jpg' },
        { title: "Director's Cut", num: 17, times: 53, img: 'https://ppt.cc/fvMlwx@.jpg' },
        { title: 'Teen,Age', num: 13, times: 39, img: 'https://ppt.cc/fxXyzx@.jpg' },
        { title: 'A|1', num: 6, times: 20, img: 'https://ppt.cc/fVgE8x@.jpg' }
      ]
    }
  },
  methods: {
    activeList (type) {
      if (type === this.curList) return true
      return false
    },
    goAlbum (index) {
      if (index === 0) this.$router.push('/album')
    }
  }
}
</script>
