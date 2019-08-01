<template>
  <q-page class="flex column items-center justify-start p-x-20">
    <div class="w-100-p p-x-20">
      <ul class="music-list">
        <li class="row list-item" v-for="(item, iIndex) in list" :key="iIndex">
          <div class="col-auto l-block">
            <q-avatar size="111px">
              <img :src="item.img">
            </q-avatar>
          </div>
          <div class="col r-block flex column items-start justify-center">
            <div>
              <div class="m-b-5 text-18">{{item.title}}</div>
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
    <div class="w-100-p">
      <p class="text-l-gray text-12 p-x-20">Playlist</p>
      <ul class="play-list">
        <li class="row list-item" v-for="(item, iIndex) in musicList" :key="iIndex">
          <div class="col-auto l-h-50 play-block">
            <q-btn flat round>
              <img src="~/assets/play-button.svg">
            </q-btn>
          </div>
          <div class="col flex column items-start justify-center">
            <div>
              <div class="text-14">{{item.title}}</div>
              <div class="text-10 text-l-gray">{{item.singer}}</div>
            </div>
          </div>
          <div class="col-auto l-h-50 text-l-gray w-45">
            <q-btn flat round icon="more_horiz"></q-btn>
          </div>
          <div class="col-auto l-h-50 text-l-gray w-45 text-right text-10">
            {{item.times}}
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
        { title: 'You Make My Day', num: 6, times: 3, img: 'https://ppt.cc/fls0Ex@.jpg' }
      ],
      musicList: [
        { title: 'Oh My!', times: '3:15', singer: 'SEVENTEEN' },
        { title: 'Holiday', times: '3:25', singer: 'SEVENTEEN' },
        { title: 'Come to me', times: '3:10', singer: 'SEVENTEEN (Vocal Team)' },
        { title: "What's Good", times: '2:48', singer: 'SEVENTEEN (Hip-hop Team)' },
        { title: 'MOONWAKER', times: '3:00', singer: 'SEVENTEEN (Performance Team)' },
        { title: 'Our dawn is hotter than day', times: '3:32', singer: 'SEVENTEEN' }

      ]
    }
  },
  methods: {
    activeList (type) {
      if (type === this.curList) return true
      return false
    }
  }
}
</script>
