<!-- =========================================================================================
    File Name: Movies
    Description: Movies Cards
    ----------------------------------------------------------------------------------------
    Item Name: Vuexy - Vuejs, HTML & Laravel Admin Dashboard Template
      Author: Pixinvent
    Author URL: http://www.themeforest.net/user/pixinvent
========================================================================================== -->

<template>
    <div id="demo-basic-card">
        <div class="vx-row">           
            <!-- OVERLAY CARD -->
            <div class="vx-col w-full lg:w-1/3 sm:w-1/2 mb-base" v-for="(movie_val, index) in moviesList">
                <vx-card class="overlay-card overflow-hidden">
                    <template slot="no-body">
                        <img :src="'https://image.tmdb.org/t/p/w500'+movie_val.backdrop_path" alt="user-profile-cover" class="responsive">
                        <div class="card-overlay text-white flex flex-col justify-between">
                            <h4 class="text-white mb-4">{{ movie_val.original_title }}</h4>
                            <p>{{ movie_val.original_title }}</p>
                        </div>               
                    </template>
                </vx-card>
            </div>
        </div>
    </div>
</template>

<script>
import VuePerfectScrollbar from 'vue-perfect-scrollbar'
import { videoPlayer }     from 'vue-video-player'
import VxTimeline          from '@/components/timeline/VxTimeline.vue'
import 'video.js/dist/video-js.css'


export default{
  components: {
    VuePerfectScrollbar,
    videoPlayer,
    VxTimeline
  },
  data () {
    return {
      // card 1
      moviesList: {},
      chatLog: [],
      chatMsgInput: '',
      timelineData: [
        {
          color : 'primary',
          icon  : 'PlusIcon',
          title : 'New Task Added',
          desc  : 'Bonbon macaroon jelly beans gummi bears jelly lollipop apple',
          time  : '25 Days Ago'
        },
        {
          color : 'warning',
          icon  : 'AlertCircleIcon',
          title : 'Task Update Found',
          desc  : 'Cupcake gummi bears soufflé caramels candy',
          time  : '15 Days Ago'
        },
        {
          color : 'success',
          icon  : 'CheckIcon',
          title : 'Task Finished',
          desc  : 'Candy ice cream cake. Halvah gummi bears',
          time  : '20 mins ago'
        }
      ],

      name  : '',
      email : '',
      msg   : '',

      playerOptions: {},
      settings: { // perfectscrollbar settings
        maxScrollbarLength: 60,
        wheelSpeed: .60
      }
    }
  },
  computed: {
    scrollbarTag () { return this.$store.getters.scrollbarTag }
  },
  mounted () {
    /*const scroll_el = this.$refs.chatLogPS.$el || this.$refs.chatLogPS
    scroll_el.scrollTop = this.$refs.chatLog.scrollHeight*/
    console.log(this.$el)
  },
  created () {
      // Card 7
   // this.$http.get('/third/party/api')
    this.$http.get('https://api.themoviedb.org/3/movie/top_rated?api_key=18790ca74eb15746ebae7354a2439dac&language=en-US&page=1')
      .then((response) => {
        let results = response.data.results;
        console.log("results", results); 
        this.moviesList = results; 
       })
      .catch((error)   => { console.log(error) })
  }
}
</script>
<style lang="scss">
#demo-basic-card {
    .overlay-card {
        .vx-card__collapsible-content {
            max-height: 485px;
        }
    }

    .chat-card-log {
        height: 360px;

        .chat-sent-msg {
            background-color: #f2f4f7 !important;
        }
    }

    .card-video {
        .video-js {
            height: 370px;
        }
    }
}
</style>
